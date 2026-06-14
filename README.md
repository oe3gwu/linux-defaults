# linux-defaults

Persönliche Linux-Konfigurationen und Vorlagen für Systemdienste. Enthält angepasste Bash- und Vim-Konfigurationen sowie Boilerplate-Dateien für Systemd- und SysV-Init-Dienste.

## Inhalt

| Datei | Beschreibung |
|---|---|
| [`.bashrc`](.bashrc) | Angepasste Bash-Konfiguration mit farbigem Prompt und Aliases |
| [`.vimrc`](.vimrc) | Vim-Konfiguration mit Syntax-Highlighting und Editor-Einstellungen |
| [`systemd.service`](systemd.service) | Vorlage für einen Systemd-Dienst |
| [`sysvinit-service`](sysvinit-service) | Vorlage für ein SysV-Init-Skript |

## `.bashrc`

Basiert auf der Standard-Debian/Ubuntu-`.bashrc` und ergänzt sie um:

- **Baum-Prompt** — mehrzeiliger Prompt mit Box-Drawing-Zeichen (`┌──`, `└─`)
- **Farben** — grüner Prompt für normale Benutzer, blau/rot für root
- **Farbige Ausgabe** — `ls`, `grep`, `diff`, `ip` und `less`/`man` mit Farbunterstützung
- **Aliases** — `ll`, `la`, `l`

### Installation

```bash
cp .bashrc ~/.bashrc
# oder per Symlink:
ln -sf "$(pwd)/.bashrc" ~/.bashrc
```

Änderungen werden in der nächsten interaktiven Shell-Sitzung wirksam, oder sofort mit:

```bash
source ~/.bashrc
```

## `.vimrc`

Vim-Konfiguration für die Terminal-Nutzung mit folgenden Einstellungen:

- **Syntax & Einrückung** — Syntax-Highlighting, dateitypspezifische Einrückung, Perl-Folding
- **Darstellung** — dunkler Hintergrund, Zeilen- und Spaltenhervorhebung, Statuszeile (`ruler`), Klammer-Matching
- **Tabs & Leerzeichen** — Tabs als 3 Leerzeichen (`expandtab`, `ts=3`, `sw=3`)
- **Suche** — case-insensitive Suche, ohne dauerhaftes Highlighting (`nohlsearch`)
- **Sonstiges** — trailing Whitespace beim Speichern entfernen, F5 togglet Paste-Modus

### Installation

```bash
cp .vimrc ~/.vimrc
# oder per Symlink:
ln -sf "$(pwd)/.vimrc" ~/.vimrc
```

## `systemd.service`

Vorlage für einen Systemd-Dienst. Platzhalter in eckigen Klammern vor der Verwendung ersetzen:

| Platzhalter | Bedeutung |
|---|---|
| `[yourdirectory]` | Arbeitsverzeichnis des Dienstes |
| `[service]` | Name und Pfad des auszuführenden Programms |
| `[options]` | Kommandozeilenoptionen |
| `[ENV]=[Variable]` | Umgebungsvariablen |

### Installation

```bash
# Datei anpassen, dann:
sudo cp systemd.service /etc/systemd/system/mein-dienst.service
sudo systemctl daemon-reload
sudo systemctl enable --now mein-dienst
```

## `sysvinit-service`

Vorlage für ein klassisches SysV-Init-Skript (Debian/Ubuntu mit `update-rc.d`). Platzhalter vor der Verwendung ersetzen:

| Platzhalter | Bedeutung |
|---|---|
| `<NAME>` | Dienstname (Dateiname, PID-Datei, Log) |
| `<COMMAND>` | Auszuführendes Kommando |
| `<USERNAME>` | Benutzer, unter dem der Dienst läuft |
| `<DESCRIPTION>` | Kurzbeschreibung im Init-Header |

Unterstützte Befehle: `start`, `stop`, `status`, `restart`, `uninstall`

### Installation

```bash
# Datei anpassen, dann:
sudo cp sysvinit-service /etc/init.d/mein-dienst
sudo chmod +x /etc/init.d/mein-dienst
sudo update-rc.d mein-dienst defaults
sudo service mein-dienst start
```

## Lizenz

Keine explizite Lizenz angegeben. Bei Verwendung oder Weitergabe bitte den Repository-Inhaber kontaktieren.
