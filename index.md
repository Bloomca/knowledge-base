# Create python env with venv

Environments are usually located outside of the projects, like `~/environments`.
To create it:

```sh
cd ~/environments
python3 -m venv your-env
source ~/environments/your-env/bin/activate
```

After that, when you install dependencies, they will be installed in `~/environments/your-env`.
