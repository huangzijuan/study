dev_3Dtheme_preview_no_ad


# raw build script
subdir=${JOB_NAME}
publish_apk_name=${JOB_NAME}.apk
#channel_cfg_file=tools/channels_full.txt
channel_cfg_file=tools/channel_honour.txt


##################################
## config
package_prefix=keyboard_theme_${appname}_

keystore_dir=/mnt/build_disk/hudson/build_env/cm_keyboard_theme/key_keyboard_theme
copy_root_dir=/mnt/build_disk/build_out_root/release_apks
work_root_dir=/mnt/build_disk/hudson/workspace
hudson_workspace=workspace
copy_dir=$copy_root_dir/${subdir}
work_dir=$work_root_dir/${subdir}
target_dir=$work_dir/${hudson_workspace}
export PATH=$PATH:/mnt/build_disk/hudson/tools_gradle_build/android-sdk-linux/tools/:/mnt/build_disk/hudson/tools_gradle_build/android-sdk-linux/platform-tools/:/mnt/build_disk/hudson/tools_gradle_build/android-sdk-linux/build-tools/24.0.0/
export ANDROID_HOME=/mnt/build_disk/hudson/tools_gradle_build/android-sdk-linux
export NDK_HOME=/mnt/build_disk/hudson/tools_gradle_build/android-sdk-linux/android-ndk-r10b
echo "$NDK_HOME"
# set jdk 1.8
#export JAVA_HOME=/mnt/build_disk/hudson/jdk1.8.0_111
#export JRE_HOME=/mnt/build_disk/hudson/jdk1.8.0_111/jre
#export CLASS_PATH=/mnt/build_disk/hudson/jdk1.8.0_111/lib:/mnt/build_disk/hudson/jdk1.8.0_111/jre/lib
#export PATH=/mnt/build_disk/hudson/jdk1.8.0_111/bin:$PATH
##################################

#echo $copy_dir/${BUILD_ID}
#exit 1
##################################
## prepare & build first apk
java -version
echo "current path: `pwd`"
cd ..
rm -rf $target_dir
mkdir -p $target_dir
cp -r $hudson_workspace $work_dir
cd $target_dir

if [ 1 = "$DefaultKeystore" ]; then
     cp $keystore_dir/cmkeyboardtheme.keystore ./
     cp $keystore_dir/use_official_key2.sh ./
elif [ 2 = "$DefaultKeystore" ]; then
     cp $keystore_dir/cmkeyboardtheme2.jks ./cmkeyboardtheme.keystore
     cp $keystore_dir/use_official_key2.sh ./
elif [ 3 = "$DefaultKeystore" ]; then
     cp $keystore_dir/cleanmaster.key ./
     cp $keystore_dir/cm_keyboard_key3.sh ./use_official_key2.sh
elif [ 4 = "$DefaultKeystore" ]; then
     cp $keystore_dir/wallpaperbackground.keystore ./
     cp $keystore_dir/cm_keyboard_theme_key4.sh ./use_official_key2.sh
fi

./use_official_key2.sh

if [ true = "$is3DTheme" ]; then
     sed -i -e 's/\"KEYBOARD_THEME_SUPPORT_3D\" android:value=\"false\"/\"KEYBOARD_THEME_SUPPORT_3D\" android:value=\"true\"/g' app/src/main/AndroidManifest.xml
fi
if [ true = "$is3DTheme2" ]; then
     sed -i -e 's/\"KEYBOARD_THEME_SUPPORT_3D\" android:value=\"false\"/\"KEYBOARD_THEME_SUPPORT_3D_COMPAT\" android:value=\"true\"/g' app/src/main/AndroidManifest.xml
     sed -i -e 's/1_0/2_0/g' app/src/main/AndroidManifest.xml
fi
sed -i -e 's/android:value=\"1_0\"/android:value=\"'"$theme_version"'_0\"/g' app/src/main/AndroidManifest.xml


chmod +x gradlew

official_apk_filename=${package_prefix}${BUILD_ID}.apk



##echo $package
##echo $appname
##echo $tid
##echo $versionCode
##echo $versionName

##echo $copy_dir/$package/${BUILD_ID}
##echo $official_apk_filename

echo sdk.dir=/mnt/build_disk/hudson/tools_gradle_build/android-sdk-linux > ./local.properties
python make.py $package "$appname" "$tid" "$versionCode" "$versionName" $copy_dir/$package/${BUILD_ID} "$official_apk_filename"


#copy to ftp
cd $copy_dir
lftp -c "open -u keyboard,keyboard123 10.60.80.70;mirror -R $package/${BUILD_ID} release_apks/${subdir}/$package/${BUILD_ID};bye"
cd ..
rm -rf $copy_dir
