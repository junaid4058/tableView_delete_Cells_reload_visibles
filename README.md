# tableView_delete_Cells_reload_visibles

# Look at this button action

 func onDeleteBtnPresed(sender : UIButton) {
        
        print(sender.tag)
        let indexpath = IndexPath.init(row: sender.tag, section: 0)

        tableView.beginUpdates()
        dataArray.remove(at: indexpath.row)
        tableView.deleteRows(at: [indexpath], with:.automatic)
        tableView.endUpdates()
        //The reason for doing this is,After deleting the particular row we need to reload table
        //Reason:
        //Just comment out the below lines and put self.tableView.reloadRows(...) just after the endupdates().
        //Then continue to delete rows one by one and see the effect
        //This is just a delay between two functions to see the delete animation and afterthat reload only visible cells not whole
        //Tableview because if you have millions data in your tableview and call reloaddata() it will call cellforrowatindexpath
        //for millions data
        let when = DispatchTime.now() + 0.3 
        DispatchQueue.main.asyncAfter(deadline: when) {
            self.tableView.reloadRows(at:self.tableView.indexPathsForVisibleRows!, with: .none)
        }
        
    }
