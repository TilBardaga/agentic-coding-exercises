# Setup Guide: Installatie van vereiste tools voor de Agentic Coding Workshop

Welkom bij de **Agentic Coding Workshop** van **Project Impact**! Voordat we beginnen, zorgen we dat alle tools geïnstalleerd zijn. Volg de stappen hieronder in volgorde voor alles wat je nog niet hebt.

---

## 1. Python 3.10+

**macOS/Windows:**

Download en voer de installer uit via https://www.python.org/downloads/

> Let op bij Windows: vink **"Add Python to PATH"** aan tijdens de installatie!

**Linux:**

Python is meestal al geïnstalleerd. Check de versie:

```bash
python3 --version
```

**Controleer installatie:**

```bash
python3 --version  # Moet 3.10 of hoger tonen
```

Meer info: [Officiële Python Downloads](https://www.python.org/downloads/)

---

## 2. UV (Python Package Manager)

**macOS/Linux:**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows (PowerShell):**

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Alternatief (Homebrew):**

```bash
brew install uv
```

**Controleer installatie:**

```bash
uv --version
```

Meer info: [Officiële UV Installatiehandleiding](https://docs.astral.sh/uv/getting-started/installation/)

---

## 3. Node.js & npm

**Aanbevolen: Officiële Installer**

- Download van: https://nodejs.org/
- Kies de LTS (Long Term Support) versie
- npm wordt automatisch meegeïnstalleerd

**Alternatief (macOS - Homebrew):**

```bash
brew install node
```

**Alternatief (Windows - Chocolatey):**

```bash
choco install nodejs
```

**Controleer installatie:**

```bash
node --version
npm --version
```

Meer info: [Officiële Node.js Downloads](https://nodejs.org/en/download/)

---

## 4. AI coding assistent

Installeer de **AI coding assistent** die je tijdens de workshop gebruikt (IDE-plugin, desktop-app, of CLI)—volg daarbij de officiële documentatie van jouw tool.

**Controleer** dat je de assistent vanuit je projectmap (of IDE) kunt gebruiken. Er is geen specifieke merk-CLI verplicht voor deze oefeningen.

---

## 5. VS Code (Aanbevolen)

**Alle Platformen:**

- Download de installer voor jouw OS: https://code.visualstudio.com/download
- Voer de installer uit
- Volg de installatie-wizard

**Controleer installatie:**

```bash
code --version
```

Meer info: [Officiële VS Code Downloads](https://code.visualstudio.com/download)

---

## 6. Git

**macOS:**

Git wordt automatisch geïnstalleerd wanneer je het voor het eerst aanroept. Typ in je terminal:

```bash
git --version
```

Als Git nog niet geïnstalleerd is, krijg je een pop-up om de Xcode Command Line Tools te installeren. Alternatief via Homebrew:

```bash
brew install git
```

**Windows:**

- Download van: https://git-scm.com/download/win
- Voer de installer uit

**Linux (Ubuntu/Debian):**

```bash
sudo apt install git-all
```

**Linux (Fedora/RHEL):**

```bash
sudo dnf install git-all
```

**Controleer installatie:**

```bash
git --version
```

Meer info: [Officiële Git Installatiehandleiding](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

---

## Laatste controle

Voer alle commands uit om te verifiëren dat alles geïnstalleerd is:

```bash
python3 --version    # Moet 3.10+ tonen
uv --version         # Moet versienummer tonen
node --version       # Moet versienummer tonen
npm --version        # Moet versienummer tonen
code --version       # Moet versienummer tonen
git --version        # Moet versienummer tonen
```

**Alle commands tonen een versienummer? Dan ben je klaar om te beginnen!**

**Krijg je "command not found"?** Herstart je terminal en probeer opnieuw. Werkt het nog steeds niet? Vraag je AI coding assistent om hulp. Meestal is het enige dat ontbreekt het updaten van je PATH-omgevingsvariabele.

---

## Alternatieve AI Coding Assistenten

Deze workshop leert frameworks die werken met **elke** AI coding assistent, bijvoorbeeld:

- **Cursor**: https://cursor.sh/
- **GitHub Copilot**: https://github.com/features/copilot
- **Aider**: https://aider.chat/

Gebruik waar je je prettig bij voelt.

---

## Hulp nodig?

- Bekijk de officiële documentatie via de links hierboven
- Stel je vragen tijdens de workshop aan Dennis Claassen of Joppe van der Schoot

**Installatietijd:** 20-30 minuten vanaf nul is normaal. Zorg dat je dit **voor** de workshop gedaan hebt!
