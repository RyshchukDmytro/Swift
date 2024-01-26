What is CoreData?

CoreData is like a storage for iOS/macOS applications that helps to store information.

**Places where to learn:**
- Kodeco
- YouTube
- Books

```
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
