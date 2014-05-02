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

Assuming you had initialized you AEM instance, navigate to the folder containing compressed vault tool:
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
First of all, you need to provide your credentials of your AEM instance.  If you are using the default username and password, just run the follow line.  Otherwise, replace the <username> and <password> with your own.
```sh
vlt --credentials admin:admin # the format goes like: vlt --credentials <username>:<password>
```

Once your credential is properly set, you can checkout (co) the files from your AEM instance.  The process may take a while depends on the size and amount of contents on your instance.
```sh
vlt co --force http://localhost:4502/crx # the format goes like: vlt co --force <uri>:<port>/crx
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