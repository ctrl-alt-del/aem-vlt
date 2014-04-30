aem-vlt
======

# About

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


