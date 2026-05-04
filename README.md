# Delphi Syntax Highlight

[![Version](https://img.shields.io/badge/version-1.1.0-blue.svg)](https://github.com/)
[![VS Code](https://img.shields.io/badge/VS%20Code-%5E1.60.0-blueviolet.svg)](https://code.visualstudio.com/)
[![Language](https://img.shields.io/badge/language-Delphi%20%2F%20Object%20Pascal-red.svg)](https://www.embarcadero.com/products/delphi)

Cette extension apporte un support de coloration syntaxique complet pour le langage **Delphi (Object Pascal)** dans Visual Studio Code. Elle a été conçue pour offrir une expérience de lecture fluide, proche de celle de **RAD Studio**, tout en profitant de la puissance des thèmes de VS Code.

---

## ✨ Fonctionnalités

L'extension couvre l'ensemble des éléments syntaxiques du langage Delphi, basée sur la documentation officielle **RAD Studio Sydney (10.4+)** et la référence **Free Pascal** :

### Commentaires
- Commentaires de ligne `// ...`
- Commentaires de bloc `{ ... }` (avec imbrication)
- Commentaires de bloc `(* ... *)` (avec imbrication)

### Directives de compilation `{$...}`
- **Conditionnelles** : `{$IFDEF}`, `{$IFNDEF}`, `{$IF}`, `{$ELSEIF}`, `{$ELSE}`, `{$ENDIF}`, `{$DEFINE}`, `{$UNDEF}`
- **Paramétriques** : `{$I fichier.inc}`, `{$R ressource.res}`, `{$L objet.obj}`, `{$APPTYPE}`
- **Switches** : `{$R+}`, `{$O-}`, `{$ALIGN ON}`, `{$HINTS OFF}`, `{$WARN ...}`, etc.

### Mots-clés
| Catégorie | Exemples |
|---|---|
| Contrôle de flux | `if`, `then`, `else`, `while`, `for`, `repeat`, `case`, `try`, `except`, `finally`, `raise` |
| Structure | `begin`, `end`, `asm` |
| Déclarations | `unit`, `interface`, `implementation`, `uses`, `var`, `const`, `type`, `procedure`, `function` |
| OOP | `class`, `record`, `object`, `interface`, `helper`, `inherited`, `constructor`, `destructor` |
| Visibilité | `private`, `protected`, `public`, `published`, `strict` |
| Modificateurs | `virtual`, `override`, `overload`, `abstract`, `sealed`, `inline`, `static`, `dynamic`, `final` |
| Conventions d'appel | `stdcall`, `cdecl`, `pascal`, `register`, `safecall`, `winapi`, `external`, `varargs` |
| Opérateurs logiques | `and`, `or`, `xor`, `not`, `is`, `as`, `in`, `shl`, `shr`, `div`, `mod` |

### Types de données natifs
- **Entiers** : `Integer`, `Cardinal`, `Int64`, `UInt64`, `Byte`, `Word`, `NativeInt`, `NativeUInt`, `Int8`..`Int32`, `UInt8`..`UInt32`, `DWORD`, `THandle`...
- **Flottants** : `Single`, `Double`, `Extended`, `Currency`, `Real`, `Comp`
- **Booléens** : `Boolean`, `ByteBool`, `WordBool`, `LongBool`
- **Chaînes** : `String`, `AnsiString`, `UnicodeString`, `WideString`, `RawByteString`, `UTF8String`, `PChar`, `PWideChar`...
- **Variants** : `Variant`, `OleVariant`, `TVarData`
- **Pointeurs** : `Pointer`, `PByte`, `PInteger`, `PChar`...
- **Objets de base** : `TObject`, `TClass`, `IInterface`, `TGUID`, `TDateTime`...

### Constantes prédéfinies
`True`, `False`, `nil`, `MaxInt`, `Pi`, `NaN`, `Infinity`...

### Fonctions et procédures système (~100)
`Assigned`, `SizeOf`, `Length`, `High`, `Low`, `Inc`, `Dec`, `Ord`, `Chr`, `SetLength`, `FreeAndNil`, `Move`, `FillChar`, `New`, `Dispose`...

### Variables de langage spéciales
`Self`, `Result`, `inherited`

### Chaînes et caractères
- Chaînes entre guillemets simples `'...'` avec échappement `''`
- Caractères littéraux `#65`, `#$41`
- Identifiants échappés `&begin`, `&type` (mots réservés utilisés comme identifiants)

### Nombres
- Décimaux : `42`, `3.14`, `1.5e-10`
- Hexadécimaux : `$FF`, `$0A1B`
- Binaires : `%1010` *(Free Pascal)*
- Octaux : `&17` *(Free Pascal)*

### Attributs RTTI
Reconnaissance des attributs entre crochets : `[SomeAttribute]`, `[assembly: SomeAttribute(param)]`

### Hints / Marqueurs de plateforme
`deprecated`, `platform`, `experimental`, `library`, `unsafe`

### Bloc assembleur inline
Dans un bloc `asm...end` : coloration des **registres** (`EAX`, `RAX`, `XMM0`...), **mnémoniques** (`MOV`, `PUSH`, `CALL`, `FILD`...) et **spécificateurs de taille** (`DWORD PTR`, `QWORD`...).

---

## 📋 Prérequis

Aucune dépendance externe n'est requise. L'extension est autonome et fonctionne immédiatement après l'installation.

> **VS Code** `^1.60.0` minimum.

---

## 📂 Fichiers reconnus

| Extension | Type de fichier |
|---|---|
| `.pas` | Unités Delphi |
| `.dpr` | Fichier projet Delphi |
| `.dpk` | Paquet Delphi |
| `.inc` | Fichier d'inclusion |
| `.pp` | Unité Free Pascal |
| `.lpr` | Fichier projet Lazarus |

---

## ⚙️ Paramètres de l'extension

Cette extension ne modifie aucun paramètre global de VS Code. Elle s'active automatiquement pour les extensions de fichiers listées ci-dessus.

La configuration du langage (`language-configuration.json`) fournit :
- **Commentaires automatiques** : `Ctrl+/` pour `//`, `Shift+Alt+A` pour `{ }`.
- **Fermeture automatique** des paires : `{ }`, `[ ]`, `( )`, `' '`.
- **Entourage de sélection** avec les mêmes paires.
- **Indentation intelligente** après `begin`, `then`, `do`, `repeat`, etc.
- **Folding** (repliement de code) : blocs `begin...end`, `{$REGION}...{$ENDREGION}`.

---

## 🐛 Problèmes connus

- **`begin...end` comme auto-closing pair** : VS Code ne supporte pas nativement les paires multicaractères (`begin`/`end`). Ce comportement est simulé mais peut ne pas se déclencher dans tous les contextes.
- **Sensibilité à la casse des thèmes** : Bien que Delphi soit insensible à la casse et que l'extension utilise le flag `(?i)`, certains thèmes peuvent rendu différemment selon la casse du code source.
- **Directives sur plusieurs lignes** : Les directives `{$...}` sont supposées tenir sur une seule ligne. Une directive multi-ligne peut ne pas être entièrement colorée.
- **Assembleur inline complexe** : Seuls les mnémoniques et registres x86/x64 les plus courants sont reconnus. Les instructions SIMD avancées (AVX-512...) ne sont pas toutes couvertes.

---

## 📋 Notes de version

### 1.1.0
- Ajout du support des fichiers `.pp`, `.lpr` (Lazarus / Free Pascal).
- Ajout des types entiers étendus : `Int8`, `Int16`, `Int32`, `UInt8`, `UInt16`, `UInt32`, `UInt64`, `NativeUInt`, `THandle`, `DWORD`...
- Ajout des types chaîne étendus : `RawByteString`, `UTF8String`, `PAnsiChar`, `PWideChar`, `PUTF8Char`...
- Ajout de ~100 fonctions et procédures système intégrées.
- Ajout des constantes prédéfinies : `True`, `False`, `nil`, `MaxInt`, `Pi`, `NaN`, `Infinity`.
- Ajout de la coloration des variables de langage spéciales : `Self`, `Result`, `inherited`.
- Ajout du bloc `asm...end` avec registres x86/x64, mnémoniques et spécificateurs.
- Ajout des attributs RTTI `[...]`.
- Ajout des directives de compilation en 3 niveaux de coloration (conditionnelles / paramétriques / switches).
- Ajout des hints de langage : `deprecated`, `platform`, `experimental`, `unsafe`.
- Ajout des identificateurs échappés `&keyword`.
- Ajout des nombres binaires (`%1010`) et octaux (`&17`) pour Free Pascal.
- Correction : les commentaires `{...}` ne capturent plus les directives `{$...}`.
- Correction : les opérateurs de comparaison sont ordonnés du plus long au plus court (`<>`, `<=`, `>=` avant `<`, `>`, `=`).

### 1.0.0
- Version initiale.
- Grammaire TextMate de base pour Delphi.
- Configuration de l'indentation et des paires automatiques.
- Support des types de données RAD Studio Sydney.

---

## 🛠️ Guide de développement local

### Structure du projet

```
delphi-syntax/
├── syntaxes/
│   └── delphi.tmLanguage.json   ← Grammaire TextMate principale
├── language-configuration.json  ← Config brackets, commentaires, indentation
├── package.json                 ← Manifeste de l'extension VS Code
└── README.md
```

### Modifier et tester l'extension

1. Ouvrez le dossier du projet dans VS Code.
2. Modifiez `./syntaxes/delphi.tmLanguage.json`.
3. Appuyez sur **`F5`** pour ouvrir une fenêtre hôte d'extension.
4. Ouvrez un fichier `.pas` dans cette fenêtre.
5. Utilisez **`Ctrl+Shift+P`** → `Developer: Inspect Editor Tokens and Scopes` pour inspecter les scopes assignés à chaque token et déboguer la grammaire.
6. Rechargez la fenêtre hôte avec **`Ctrl+R`** après chaque modification.

### Installer localement (sans publication)

Copiez le dossier complet dans :

| Système | Chemin |
|---|---|
| Windows | `%USERPROFILE%\.vscode\extensions\delphi-syntax-1.1.0` |
| macOS | `~/.vscode/extensions/delphi-syntax-1.1.0` |
| Linux | `~/.vscode/extensions/delphi-syntax-1.1.0` |

Puis redémarrez VS Code.

### Publier sur le Marketplace

```bash
npm install -g @vscode/vsce
vsce package      # génère un fichier .vsix
vsce publish      # nécessite un compte Azure DevOps + Personal Access Token
```

---

**Bon code avec Delphi ! 🎯**