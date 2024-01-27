# CoreData

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

func fetchPeople() {
    do {
        self.items = try context.fetch(Person.fetchRequest())

        Dispatch.main.async {
            self.tableView.reloadData()
        }
    } catch {

    }
}
```

**To create object**
```swift
let newPerson = Person(context: self.context)
newPerson.name = texfield.text
```

**To save object**
```swift
do {
    try self.context.save()
} catch {

}
```

**To fetch(refresh) data**
```swift
self.fetchPeople()
```

**To delete data**
```swift
let personToRemove = self.items![indexPath.row]

self.context.delete(personToRemove) <<== this row

do {
    try self.context.save()
} catch {

}
self.fetchPeople()
```

**To edit data**
```swift
let person = self.items![indexPath.row]

person.name = textfield.text <<== this row

do {
    try self.context.save()
} catch {

}
self.fetchPeople()
```

**To filter and sort CoreData**
```swift
let context = (UIApplication.shared.delegate as! AppDelage).persistetContainer.viewContext

func fetchPeople() {
    do {
        let request = Person.fetchRequest() as NSFetchRequest<Person>

        // Set the filtering
        let pred = NSPredicate(format: "name CONTAINS 'Dmytro'") || let pred = NSPredicate(format: "name CONTAINS %@", "Dmytro")
        request.predicate = pred

        // Set sorting on the request
        let sort = NSSortDescriptor(key: "name", ascending: true)
        request.sortDescriptor = [sort] <<== it's array so we can sort with multiply sort conditions (ex. by name and surname)

        self.items = try context.fetch(request)

        Dispatch.main.async {
            self.tableView.reloadData()
        }
    } catch {

    }
}
```

**With multiply Entities**
Create **Person** and **Family** Entities. In Family we create relationship with Person entity
- **destination** Person
- **inverse** family
- **Type** To Many
```swift
func relationships() {
    let family = Family(context: context)
    family.name = "Ukraine"

    let person = Person(context: context)
    person.name = "Ua"

    family.addPerson(person) || person.family = "Ukraine"

    try! context.save() || with do-try-catch
}
```

**Codegen** in xcdatamodeId
- Manual/None -> We need to manually create and update our [**Model+CoreDataClass**] and [**Model+CoreDataProperties**] so later we can modify those files as we want
- Class Definition -> XCode will generate [**Model+CoreDataClass**] and [**Model+CoreDataProperties**] automaticaly, but we can't see and modify those files
- Category/Extension -> We need to create only [**Model+CoreDataClass**] so we can modify it later
