# TableView

**Delete something from tableview**
```swift
func tableView(_ tableView: UITableView, trailingSwipeActionsConfigurationForRowAtindexPath: IndexPath) -> UISwipeActionsConfiguration? {
  let action = UIContextualAction(style: .destructive, title: "Delete") { (action, view, completionHandler) in
    ... = <<  delete action here, usually from database
  }
  return UISwipeActionsConfiguration(actions: [action])
}
```

**Make some action after swipe tableview**
```swift
func tableView(_ tableView: UITableView, leadingSwipeActionsConfigurationForRowAt indexPath: IndexPath) -> UISwipeActionsConfiguration? {
  return UISwipeActionsConfiguration(actions: [makeCompleteContextualAction(forRowAt: indexPath)])
}

private func makeCompleteContextualAction(forRowAt indexPath: IndexPath) -> UIContextualAction {
  return UIContextualAction(style: .normal, title: "Complete") { (action, swipeButtonView, completion) in
    action.image = ProjectImages.Annotation.checkmark
    action.image?.withTintColor(.systemGreen)
    action.backgroundColor = .systemOrange
    print("COMPLETE HERE")
    completion(true)
  }
}
```
