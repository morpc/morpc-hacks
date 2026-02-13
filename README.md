# morpc-hacks
Low-code or no-code hacks useful for working with MORPC data

## Combining the rows from similar CSV files

Say you have a bunch of similar CSV files (i.e. CSV files having the same exact columns) and you'd like to combine the rows to make one long CSV file.  You could open the files in Excel one by one and copy and paste the contents into a new file, or you could try this.  

  - Put all of the CSV files you want to combine in the same directory. **Get rid of all other CSV files in that directory** (this is important to ensure that only the desired files are combined).
  - Open Windows command prompt
    - Launch the "Run" dialog by holding the `Windows` key and pressing the `R` key
    - Type `cmd` in the run dialog and click "OK".  The command prompt window will open.
  - Verify that the prompt starts with "C:\".  If NOT, type `C:\` and press `Enter`.
  - Type `cd` followed by a space followed by the path to the folder where the CSV files are located.  You can get the path a couple ways:
    - Option 1: Navigate to the folder in in Windows Explorer (i.e. the file browser). Copy the path from the address bar.
    - Option 2: Navigate so that you can *see* the folder itself in Windows Explorer.  Right click on the folder and select "Copy as path" from the context menu.
    - For either option, you can paste the path by right-clicking in the command prompt window.  If the path is not enclosed in quotes (`"`), add them to the start and end of the path to ensure Windows handles spaces in the path properly. The command should look something like this: `cd "C:\Users\someuser\myfolder"` (exact path may vary a lot depending on where you put the files)
  - Press `Enter` to finish the command and change to the folder you specified.
  - Type `dir` and press `Enter` to list the contents of the folder. Make sure you see your CSV files.  Note the first file in the list. For the sake of instruction, let's say it is `myfile1.csv`. Wherever you see `myfile1.csv` below, replace it with the actual file name.
  - Open `myfile1.csv` in Excel or a text editor. Choose a word in the first row/line that you do not expect to appear in the data (i.e. the non-header rows) of any file.  We'll call this `filterWord`.  Wherever you see `filterWord` below, replace it with the actual word you chose.
  - Enter the following command, then press `Enter`. This will copy the header row only to a new file called `combined.txt`: `findstr filterWord myfile1.csv > combined.txt`
  - Enter the following command, then press `Enter`. This will copy all of the rows *except* the header rows from all of the CSV files to the new file: `findstr /V filterWord *.csv >> combined.txt`
  - Enter the following command, then press `Enter`. This will rename the new file so that it has a ".csv" extension: `move combined.txt combined.csv`
  - In the file browser, in the folder containing the CSV files, open the file called 'combined.csv'.  Verify that it contains only one instance of the header row (in the first row) and that it includes all of the data from the individual CSVs.
  - You're done!  Feel free to rename 'combined.csv' to something else if you like.
  - If you need to try again, be sure to delete 'combined.csv' first or else it too will be included in the combined output.

Caveats: This will not work right in the following cases.
  - If the files are .xls or .xlsx files.  They must be text files (CSV, tab-delimited, or similar)
  - If the header string that you choose is also present in the data rows.  In that case those rows will be omitted from the output.
