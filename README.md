# Maintaining multiple angular applications in a single workspace.

# 1. Create an empty workspace :
    ng new <workspace_name> --createApplication=false --directory=multiApps --interactive=false

The --createApplication=false parameter avoids the creation of an initial application (default value is true). Otherwise, the Angular CLI creates an application in the src folder of the new workspace. It’s cleaner to generate all applications in the sub-folder projects of the workspace.

The --interactive=false parameter is just here to avoid being prompted for useless parameter values such as whether the initial app (which we don’t generate) should include a routing module or what CSS preprocessor to use.

The --directory=frontend parameter is the directory name to create the workspace in. It defaults to the workspace name.

# 2. Create application within workspace:

    ng g application admin --style=scss --routing=true
    ng g application front --style=scss --routing=true
    ng g application shared --style=scss --routing=false
    ...

# 3. Create libraries in workspace:
cd <workspace_name>
    ng generate library tools
    ng generate library vendors

-- we can check the structure in the config file angular.json

# 4. Create a shared service
cd <workspace_name>
    ng generate service hello-world --project=tools

# 5. Launching the application
cd <workspace_name>
    ng serve --project=admin

    5.1 Serving Angular Apps on Specific Port and Base Href
    - configure port(say 4222) in options object contained in serve in project name in angular.json, then run
    ng serve --open --project=front --baseHref /front/
    app witll start running on http://localhost:4222/front

