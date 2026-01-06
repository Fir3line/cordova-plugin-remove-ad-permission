var fs = require("fs");
var path = require("path");

var rootdir = "";
var manifestFile = path.join(rootdir, "platforms/android/app/src/main/AndroidManifest.xml");

fs.readFile(manifestFile, "utf8", function (err, data) {
    if (err)
        return console.log(err);

    // If already present, do nothing
    if (data.indexOf('android:largeHeap="true"') !== -1) {
        console.log('[manifest-hook] android:largeHeap already present.');
        return;
    }

    // Inject android:largeHeap="true" into <application> opening tag
    var result = data.replace(
        "<application",
        '<application android:largeHeap="true"'
    );

    if (result === data) {
        console.log('[manifest-hook] <application> tag not found, nothing changed.');
    } else {
        console.log('[manifest-hook] Injected android:largeHeap="true".');
    }

    fs.writeFile(manifestFile, result, "utf8", function (err) {
        if (err)
            return console.log(err);
    });
});
