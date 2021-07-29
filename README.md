# Docfx-template Introducation
DocFX can produce documentation from source code including C#, F#, Visual Basic, REST, JavaScript, Java, Python and TypeScript as well as raw Markdown files.

# Installing Docfx
## Installing on Windows
### Installing prerequisites
1. First, ensure that you are using an administrative power shell.
2. Run Get-ExecutionPolicy. If it returns Restricted, then run Set-ExecutionPolicy AllSigned.
3. Run `Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`
4. Run `choco install docfx -y`
5. Run `choco install wkhtmltopdf`

# Create documentation from the standard template
1. Create a new folder
2. From the folder call `docfx init -q`. This command generates a docfx_project folder with the default docfx.json file under it.
3. Use `docfx docfx.json` to build the site.
4. Use `docfx serve docfx_project/_site` or `docfx --serve` to host the site locally.
5. 

# How to add code to the docfx.json for documentation generation
1. First add the code, preferably as a sub-module to the src folder.
2. Then in the `metadata` object add the following object:
```
{
      "src": [
        {
          "files": [
            "src/project-name/**.csproj"
          ]
        }
      ],
      "dest": "project-name",
      "disableGitFeatures": false,
      "disableDefaultFilter": false
}
```
3. To also include the code in the new build add the following to the `contect` object within the `build` object:
```
{
        "files": [
          "project-name/**.yml",
          "project-name/index.md"
        ]
}
```

Now, when the `docfx docfx.json` command is run, docfx is going to build the `*.yml` files required in the `project-name` folder.

# How to add the generated YML files in the documentation
The structure of the documentation is defined by the `toc.yml` located in the root folder of the documentation. In the default template this file includes:
```
- name: Articles
  href: articles/
- name: Api Documentation
  href: api/
  homepage: api/index.md
```

For the newly generated files the show up, the content of this file needs to be modified to the following:
```
- name: Articles
  href: articles/
- name: Api Documentation
  href: api/
  homepage: api/index.md
- name: Project Name
  href: ../project-name/toc.yml
```
     
    
