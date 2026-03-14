# Onshape to Robot: URDF Xacros

<p align="center">
<img src="docs/source/_static/img/main.png" />
</p>

This tool is based on the [Onshape API](https://dev-portal.onshape.com/) to retrieve
informations from an assembly and build a robot description (URDF, Xacros) mainly to make ROS2 URDF definitions easier.

## Instructions:
1. Get Onshape API key, access key and secret key from your Onshape account. Save them in your <code>~/.bashrc</code> file as:
    ```bash
    # .bashrc
    # Obtained at https://dev-portal.onshape.com/keys
    export ONSHAPE_API=https://cad.onshape.com
    export ONSHAPE_ACCESS_KEY=Your_Access_Key
    export ONSHAPE_SECRET_KEY=Your_Secret_Key
    ```

2. Install onshape-to-robot from source:
    ```bash
    git clone https://github.com/akhil-gunda/onshape-to-robot.git
    cd onshape-to-robot
    git checkout urdf_xacros
    pip install -e .
    ```

3. In your ROS2 package directory, create a file called <code>config.json</code> to configure onshape-to-robot.
    ```json
    {
         // Onshape URL of the assembly
        "url": "",
        // Output format
        "output_format": "xacro", // or URDF if an URDF is expected
        "package_name": ""
    }
    ```

4. Run onshape-to-robot in the directory of the ROS2 package:
    ```bash
    onshape-to-robot <folder where config.json is located>
    ```

5. This command creates the meshes (.stl files) under the <code>/meshes</code> directory, and a file (URDF or Xacro).



## Intended use for Onshape-to-robot xacros
### Step 1: Create sub-assemblies on Onshape
1. Split the full URDF scene assembly into sub-assemblies that you intend to compose into a full URDF using Xacros.
2. Place a mate-connector in the sub-assemblies where the other xacro must connect to.

### Step 2: For each sub-assembly, generate a xacro, using the config param (in <code>config.json</code> file)
```json
{
    "output_format": "xacro",
    "robot_name": "sub-assembly-1" // Name of the xacro file
}
```

### Step 3: Create a URDF with all the xacros manually
Manually create a URDF xacro file assembling all the xacros together.