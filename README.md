qtjambi-unofficial
==================

Collection of up-to-date qtjambi versions (>=4.8.5)

## Tested and working
- Windows x64 (with QT4.8.6 and qtjambi 4.8.5-0)
- Linux x64 (with QT4.8.6 and qtjambi 4.8.5)

## Using maven
If you want to use these libs with maven / gradle the URL is: https://raw.githubusercontent.com/git-commit/qtjambi-unofficial/mvn-repo/

The maven repo follows the naming scheme `net.sf.qtjambi:qtjambi-native-<os_id><arch>:<qtJambiVersion>`. With `arch` being either 32 or 64. To see which versions are available you can browse the above URL.

Valid `os_id` values are `win` `mac` or `linux`

Example build.gradle:
```groovy
apply plugin: 'application'

repositories {
    jcenter()
    maven {
        url "https://raw.githubusercontent.com/git-commit/qtjambi-unofficial/mvn-repo/"
    }
}

//Figure out jar name
def os_fullName = System.getProperty('os.name')
def os_split = os_fullName.toLowerCase().split()[0]
def arch = System.getProperty('os.arch').contains('64') ? '64' : '32';
def os_id

// Default QT-Jambi version
def qtJambiVersion = "4.8.5"

switch(os_split) {
    case 'windows':
        os_id = 'win'
        qtJambiVersion = '4.8.5-0'
        break
    
    case 'linux':
        os_id = os_split
        if (arch.equals('64'))
            qtJambiVersion = '4.8.6'
        break
    
    case 'mac':
        os_id = os_split
        break
    
    default:
        throw new Exception('Unsupported OS')
}

String qtJambiNative = "net.sf.qtjambi:qtjambi-native-${os_id + arch}:${qtJambiVersion}"

print("##############\n" +
        "# Debug Info #\n" +
        "##############\n\n" +
        "os.arch = ${System.getProperty('os.arch')}\n" +
        "Detected OS arch: ${arch}-Bit\n\n" +
        "os.name = ${os_fullName}\n" +
        "Detected OS: ${os_id}\n\n" +
        "Qt Jambi version: ${qtJambiVersion}\n\n")

dependencies {
    compile "net.sf.qtjambi:qtjambi:${qtJambiVersion}"
    compile qtJambiNative

    compile 'net.java.jinput:jinput:2.0.6'
    
}
```

## Special Thanks
Linux:
http://unofficial.qt-jambi.org/

Windows and OSX:
http://www.labstory.se/compiledqt/

## Donate
If this helped you and you would like to give something back in return, you can click this Flattr button or send me some bitcoins.

<a href="https://flattr.com/submit/auto?user_id=Snowdragon&url=https%3A%2F%2Fgithub.com%2Fgit-commit%2Fqtjambi-unofficial" target="_blank"><img src="http://api.flattr.com/button/flattr-badge-large.png" alt="Flattr this" title="Flattr this" border="0"></a>

Send Bitcoins to:
<pre>12LjMXVoH2MtnnaLBoZHpesZirj4JMhPvL</pre>
