# UIAlert

**Creat UIAlertController**
```swift
func addAction() {
  let alert = UIAlertController(title: "Add Person", message: "What is their name?", preferedStyle: .alert)
  alert.addTextField()

  let submitButton = UIAlertAction(title: "Add", style: .default) { (action) in
    let textField = action.textField![0]
    ... <<= some logic here
  }
  alert.addAction(submitButton)

  self.present(alert, animated: true, completion: nil)
}
```
