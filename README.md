# (WIP) Node Install Rust Binaries (NIRB)

Installs rust binaries as node dependencies using a node compatible CLI interface.

The use case is that I want to integrate an existing rust binary (not wasm) onto my system so that it runs.

This is a prototype to see if we can download rust binaries.
I'm sure this could be extended to other ecosystems.

## Usage

1. Create a new node project.
2. Install `nirb` as a runtime dependency using `npm install nirb`.
3. Call `nirb` in your `postinstall` script with the required arguments:
   ```json
   {
     "scripts": {
       "postinstall": "nirb"
     },
     "bin": {
       "package-binary": "path/to/package-binary"
     }
   }
   ```
4. Run that binary using your package manager `npm exec package-binary`.

## Use case

I created a rust backend that I want to download as a dependency of my project.
I shouldn't need rust tooling, only the tooling that I need for my node project.

If I'm on a system where I have not got a release for my target (ie. Windows),
it should download and install using build tools on the system (rustup)
so the binary is 90% available on my system.

## CLI

Internally, `nirb` needs the following information:

| Information            | Inference Rating | Notes                                                                                   |
| :--------------------- | ---------------: | :-------------------------------------------------------------------------------------- |
| Name                   |              80% | Remote rust repository could use different naming convention                            |
| Version                |              90% | Infer from `package.json`, Rust and Node have different semantic version specifications |
| Remote Binary Location |              50% | Defaults to cargo registry, but could be GitHub or another file hosting system          |
| Architecture           |             100% |                                                                                         |
| Triple                 |             100% |                                                                                         |
| Source Code Location   |               0% |                                                                                         |
| Binary Naming Scheme   |               0% |                                                                                         |

100% means we are responsibe for getting this information, and 0% means you're respsonsible for providing this information.
In between these numbers means we can try to figure it out, with higher numbers meaning we're more likely to get it right than not.

## Plugins

This is not going to be implemented yet, but could be implemented.
