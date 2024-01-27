What is CoreData?

1)
2)
3) Managed Object Context -> Transfer data from [2] to [Core Data Persistent Container]
4) Core Data Persistent Container -> Place where data is saved and can be readed.

**NSManagedOpject** class we need to transfer data to and from [Core Data Persistent Container] in understandable format (ex. Person to binary and vice versa)

**Codegen** in xcdatamodeId
- Manual/None -> We need to manually create and update our [**Model+CoreDataClass**] and [**Model+CoreDataProperties**] so later we can modify those files as we want
- Class Definition -> XCode will generate [**Model+CoreDataClass**] and [**Model+CoreDataProperties**] automaticaly, but we can't see and modify those files
- Category/Extension -> We need to create only [**Model+CoreDataClass**] so we can modify it later

CoreData is like a storage for iOS/macOS applications that helps to store information.

**Places where to learn:**
- Kodeco
- YouTube
- Books

```swift
static func addCoreData(name: String, image: URL) {
    let context = (UIApplication.shared.delegate as! AppDelegate).persistentContainer.viewContext
    let newData = MyData(context: context)
    newData.name = name
    newData.image = image
    do {
        try context.save()
    } catch {
        print("error-Saving data")
    }
}
```

