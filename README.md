# Flatpak generator for GOG installers
The hope is to have this eventually work with almost any GOG game, but that is probably a ways off.

## Prerequisites
You will need flatpak 0.9.7 or later, and python3. Both should be available in your repository if not already installed.

## Usage
To prepare a game, you can use the provided "json-maker.py" script, e.g.

`./json-maker.py ~/Downloads/gog_baldur_s_gate_2_enhanced_edition_2.6.0.11.sh`

which will create a new json in the current dir based on the com.gog.Template.json file, with a name like gen_com.gog.BaldursGate2EnhancedEdition.json .

You can then build and install it directly thus:

`flatpak-builder --user --install build gen_com.gog.BaldursGate2EnhancedEdition.json --force-clean --arch=i386`

Or build and export it to a repo before installing it:

`flatpak-builder build gen_com.gog.BaldursGate2EnhancedEdition.json --force-clean --arch=i386 --repo ~/FlatPak/gog-repo`

`flatpak --user install gog-repo com.gog.BaldursGate2EnhancedEdition`

(see also the suggested command in the output of json-maker.py)

After installation you can start it like this, or use the desktop/menu icon that should have also been created.

`flatpak run com.gog.BaldursGate2EnhancedEdition`

## Disk-space use
flatpak-builder leaves some caching in .flatpak-builder, and the prepared Build/GAMENAME directory. These can be safely removed once you have the game running.

The flatpak repo contains the games you have packaged. Don't delete this if you want to be able to reinstall the game.

If you are planning to build a lot of flatpaks, disk use will quickly balloon, as each game takes space in both the (local) flatpak repo, and when installed.

## Troubleshooting
Sometimes the start.sh script provided from GOG does not work right in our flatpak.
You can "override" this by placing a custom start-script in overrides/starter-GAMENAME .

## Compatibility
This has not been tested with many GOG games yet, and it is extremely likely that a lot of further work will be needed to cover more games.

See the [compatibility list](https://github.com/kujeger/flatpak-gog/wiki/Compatibility) for details.
