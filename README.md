# Nav2009ObjectManager
This set of files provides you with a possibility to export/import your NAV 2009 objects directly to your local repo (folder).

# Setup
1. Create your own repository (git init).
    Your repository should contain at least the following folders:
    ../iconv
    ../application files
2. Create a folder having iconv.exe file to convert your objects from cp866 to utf-8.
    You can find needed files at http://gnuwin32.sourceforge.net/packages/libiconv.htm.
    Your folder should look like
    ../iconv/

        /iconv.exe
    
        /libcharset1.dll
    
        /libiconv2.dll
    
        /libintl3.dll
3. Align objects IDs with your database IDs, compile objects;
4. Run the form "Object Manager";
5. Set values for "App Folder Path" - a path where you store your objects in .txt,
    "FOB Folder Path" (optional) - a path where you store your objects in .fob,
    "Iconv File Path" - a path where the iconv.exe is located,
    "Compilation Strategy" - a method how will you compile imported objects.
6. Export all your objects to "../application files" folder, you specified the path in "App Folder Path" value;
7. Sync your repo with "origin" (git push).

# How to export
You can export your files as text or as .fob.
Before export, you should specify the path where you want the objects to be exported.

When you run the form "Object Manager", the COD "Object Management" marks all your objects in your licence by having a "Modify Permission". So if you have permission to modify COD 1 but do not have the same for COD 10, the form will show you COD 1 and filter out COD 10. So be careful with filters and "Ctrl + Shift + F7". Always choose "Marked Only" option.

## Export as txt
When you run "Export", the form will
1. Export filtered objects to specified folder;
2. Make .bat file to convert exported objects from cp866 to utp-8;
3. Run .bat file;
4. Delete .bat file;
5. Delete temporary files in cp866.

As a result, you will have utf-8 formatted files.

## Export as FOB
When you run "Export FOB", the form will export filtered objects as .FOB files in specified folder.


# How to import
The import function works the same as the export function: it imports filtered objects.
The program will find filtered files, convert them from utf-8 to cp866, then import as text and delete temporary files. Then it will try to compile the objects.
How your objects will be compiled depends on the "Compilations Strategy" value.
If you set "Compilations Strategy" = Imported, then all your imported objects will be compiled one by one.
If you set "Compilations Strategy" = All, then all your files will be imported, then all the objects in your database will be compiled. It is useful when you want to check if you do not have destructive changes in the repo.

# Known issues
1. If your repo has a new file, it will not be imported into your database until you create it manually. It is because the NAV 2009 does not check the folder for files, it filters objects and then checks the folder for the filtered objects.
2. If you have a compilation error, your objects will not be compiled. You should fix it manually.
3. If you develop in a remote database in a local client, you set your own path to the folders. Another developer wants to use their own paths. So you should be careful while developing in a shared database.
4. It doesn't work without iconv.