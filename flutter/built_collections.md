## 特性
1. Built Collections must be created with explicit type parameters; there is no such thing as a BuiltList<dynamic>.
new BuiltList([1, 2, 3]);     // Throws an exception!
new BuiltList<int>([1, 2, 3]); // Better.
2. Values must be non-null; nulls cannot be added to a Built Collection.
new BuiltList([1, 2, null]);  // Throws an exception!
3. Built Collections are comparable and hashable. This means you can put them in maps, sets, and multimaps, creating exactly the collections to match your data.
