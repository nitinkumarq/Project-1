// Folder: src/icp_backend/src/lib.rs

use ic_cdk::query;

#[query] fn greet(name: String) -> String { format!("Hello, {}! Welcome to Internet Computer!", name) }

// Folder: src/icp_backend/Cargo.toml

[package] name = "icp_backend" version = "0.1.0" edition = "2018"

[dependencies] ic-cdk = "0.5.4" ic-cdk-macros = "0.5.4"

[lib] crate-type = ["cdylib"]

// Folder: src/icp_frontend/index.html

<!DOCTYPE html><html>
<head>
  <title>ICP Frontend</title>
</head>
<body>
  <h1>ICP Frontend</h1>
  <input id="name" placeholder="Enter your name" />
  <button onclick="greetUser()">Greet</button>
  <p id="greeting"></p>  <script type="module">
    import { greet } from "../../declarations/icp_backend/icp_backend.js";

    window.greetUser = async function () {
      const name = document.getElementById("name").value;
      const greeting = await greet(name);
      document.getElementById("greeting").innerText = greeting;
    }
  </script></body>
</html>// Folder: dfx.json

{ "canisters": { "icp_backend": { "type": "rust", "package": "icp_backend", "candid": "src/icp_backend/icp_backend.did", "wasm": "target/wasm32-unknown-unknown/release/icp_backend.wasm" }, "icp_frontend": { "type": "assets", "source": "src/icp_frontend" } }, "defaults": { "build": { "packtool": "vessel" } }, "dfx": "0.14.0", "networks": { "local": { "bind": "127.0.0.1:8000", "type": "ephemeral" } }, "version": 1 }

