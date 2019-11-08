1. 解决Failure [INSTALL_FAILED_TEST_ONLY]
adb install -t XXX.apk

2. room升级数据库写法
https://zhuanlan.zhihu.com/p/77408877

销毁与重建策略
在Sqlite中修改表结构会比较麻烦。比如我们希望将Student表中的age字段类型从INTEGER改为TEXT。

面对此类需求，最好的方式就是采用“销毁与重建策略”，该策略大致分为以下几个步骤：

1.创建一张符合我们要求的临时表temp_Student

2.将数据从旧表Student拷贝至临时表temp_Student

3.删除旧表Student

4.将临时表temp_Student重命名为Student

static final Migration MIGRATION_3_4 = new Migration(3, 4)
    {
        @Override
        public void migrate(SupportSQLiteDatabase database)
        {
            database.execSQL("CREATE TABLE temp_Student (" +
                    "id INTEGER PRIMARY KEY NOT NULL," +
                    "name TEXT," +
                    "age TEXT)");
            database.execSQL("INSERT INTO temp_Student (id, name, age) " +
                    "SELECT id, name, age FROM Student");
            database.execSQL("DROP TABLE Student");
            database.execSQL("ALTER TABLE temp_Student RENAME TO Student");
        }
    };

3.
