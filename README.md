aem-vlt
======

# About

The official instruction from Adobe is in here:
http://wem.help.adobe.com/enterprise/en_US/10-0/core/how_to/how_to_use_the_vlttool.html
Please refer to the official document if needed.


# Setup
Navigate to the directory of your AEM instance:
```sh
cd <AEM_instance_directory>
```

Assuming you had initialized you AEM instance (had ran your AEM instance before), navigate to the folder containing compressed vault tool:
```sh
cd /crx-quickstart/opt/filevault
```

Unzip the compressed vault tool:
```sh
unzip -a filevault.zip
```

Navigate to the executable vlt file inside the newly created folder:
```sh
cd <Vault_cli_folder>/bin
```

Move the executable vlt file to /usr/bin, you may need your password for the write permission:
```sh
sudo mv vlt /usr/bin/vlt
```

Alternatively, you can add the path to your .bash_profile if you don't want to move it to your /usr/bin folder, and then source the .bash_profile whenever you need to use vlt.

To add the path, open your .bash_profile by running:
```sh
sudo vim ~/.bash_profile
```

If there is an error saying "vim" is undefined or cannot be found, try running:
```sh
sudo vi ~/.bash_profile
```

Once you opened your .bash_profile on terminal, press "i" key to enter "insert mode".
Move to the last line of the file, start a new line, and then type:
```sh
export PATH=<AEM_instance_directory>/<Vault_cli_folder>/bin:$PATH
```

Once you are done, press "esc" key to exit the "insert mode", and then save your changes and exit the file by running:
```sh
:x
```

Upon you hit the "enter/return" key, you should be back to normal terminal.

Verify the path of your vlt is added by running:
```sh
echo $PATH
```

To use vlt, you need to source the .bash_profile by running:
```sh
source ~/.bash_profile
```

Now, you should be able to use vlt.


# Sync
To sync your jcr with file system, you need to have your AEM instance running.

Open your terminal and navigate to a whichever directory that is convenient to you (e.g. ~/Desktop)
```sh
cd ~/Desktop
```

Create a folder for synchonizing with AEM:
```sh
mkdir -p aem6
cd aem6
```

Once you are inside the folder you just created, you can start the sync process.
First of all, you need to provide your credentials of your AEM instance.  If you are using the default username and password, just run the follow line.  Otherwise, replace the <username> and <password> with your own.  You can checkout (co) the files from your AEM instance.  The process may take a while depends on the size and amount of contents on your instance.
```sh
vlt --credentials admin:admin co --force http://localhost:4502/crx 
# the format goes like: vlt --credentials <username>:<password> co --force <uri>:<port>/crx
```

Once the checkout is done, you can now copy the files that you want to deploy into your AEM instance to the file structure, placing them under <file_path> such as /jcr_root/etc.

Then navigate to the jcr_content folder and check the status of the files being copied into the file structure.
```sh
cd jcr_content
vlt status # should see all newly added files
```

Stage the files that you want to depoly to the AEM instance.
```sh
vlt add <file_name>
```

Then commit them.
```sh
vlt commit -v
```

The files should now be deployed to your AEM instance, and you should be able to find them on CRX-DE under the <file_path> that you specified earlier.