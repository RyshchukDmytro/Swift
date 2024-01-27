What is CoreData? CoreData is like a storage for iOS/macOS applications that helps to store information.

1)
2)
3) Managed Object Context -> Transfer data from [2] to [Core Data Persistent Container]
4) Core Data Persistent Container -> Place where data is saved and can be readed.

- In AppDelegate file we have **lazy var persistentContainer: NSPersistentContainer = { ...** that give us access to [**CoreData**]

- In AppDelegate file we have **func saveContext() {...** that check if there any updates in [**CoreData**] and save them

- **NSManagedObject** class we need to transfer data to and from [Core Data Persistent Container] in understandable format (ex. Person to binary and vice versa)

- **(UIApplication.shared.delegate as! AppDelage).persistetContainer** -> Give us access to [**Core Data Persistent Container**], but we need to do next step to get real access to [**CoreData**]

- **(UIApplication.shared.delegate as! AppDelage).persistetContainer.viewContext** -> Give us access to [**NSManagedObject** ] and now we can interact with [**Core Data Persistent Container**]

**To fetch data from CoreData**
```swift
let context = (UIApplication.shared.delegate as! AppDelage).persistetContainer.viewContext

func fetchPerson() {
    do {
        self.items = try context.fetch(Person.fetchRequest())

        Dispatch.main.async {
            self.tableView.reloadData()
        }
    } catch {

    }
}
```

**Codegen** in xcdatamodeId
- Manual/None -> We need to manually create and update our [**Model+CoreDataClass**] and [**Model+CoreDataProperties**] so later we can modify those files as we want
- Class Definition -> XCode will generate [**Model+CoreDataClass**] and [**Model+CoreDataProperties**] automaticaly, but we can't see and modify those files
- Category/Extension -> We need to create only [**Model+CoreDataClass**] so we can modify it later




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

