# TableView

**Delete something from tableview**
```swift
func tableView(_ tableView: UITableView, trailingSwipeActionsConfigurationForRowAtindexPath: IndexPath) -> UISwipeActionsConfiguration? {
  let action = UIContextualAction(style: .destructive, title: "Delete") { (action, view, completionHandler) in
    ... = <<  delete action here, usually from database
  }
  return UISwipeActionsConfiguration(action: [action])
}
```
