File = require("file");
JSON = require("json");
Jake = require("jake");

USERJS = "show_password_onfocus.user.js";
MANIFEST = "manifest.json";

function make_manifest(userjs) {
  userjs = new String(userjs);
  userjs.key = function(key) {
    var m = this.match(new RegExp("// @"+ key +"\\s+(.+)\\n"));
    return (m && m[1]) ? m[1] : "";
  };
  return {
    name: userjs.key("name"),
    description: userjs.key("description"),
    version: userjs.key("version"),
    content_scripts: [
      {
        matches: ["http://*/*", "https://*/*"],
        js: [USERJS]
      }
    ],
    icons: {
      32: "icon_32.png",
      48: "icon_48.png",
      64: "icon_64.png"
    },
    update_url: "http://clients2.google.com/service/update2/crx"
  };
}

Jake.task("default", function build_manifest_for_chrome_extension(){
  var userjs = File.read(USERJS);
  var manifest = make_manifest(userjs);
  File.write(MANIFEST, JSON.stringify(manifest, false, '  '));
  print(MANIFEST + " is done.");
});
