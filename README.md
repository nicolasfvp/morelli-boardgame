# Morelli Board Game

Java implementation of the Morelli digital board game for two players. Morelli is played on a circular board made of concentric rings, and pieces move toward the center of the board. This repository was produced as an academic software engineering exercise focused on the maintenance of a legacy system built on the NetGames multiplayer framework.

## Tech stack

- Java 8 (source and target level 1.8)
- Java Swing for the graphical user interface
- NetGames multiplayer framework (br.ufsc.inf.leobr) for the client/server networking layer
- Apache Ant with a NetBeans project layout (build.xml and nbproject/) for building
- ResourceBundle based internationalization (English and Brazilian Portuguese)

## What it does

- Runs a two player match of Morelli over a network connection using the NetGames server.
- Renders the circular board with concentric rings and handles piece placement and movement through a Swing interface.
- Moves pieces toward the center along orthogonal and diagonal lines according to the game rules.
- Captures opponent pieces when a piece is trapped between two of the current player's pieces.
- Ends the match when a player reaches the central throne or captures all opponent pieces.
- Loads interface messages in English or Portuguese depending on the runtime locale.

## Game rules

- The board is circular with seven concentric rings (numbered 0 to 6). Ring 0 is the center (the throne) and rings 1 to 6 are the outer rings with an increasing number of positions.
- Pieces can only move toward the center, that is, toward rings with a lower number.
- A move follows an orthogonal (horizontal or vertical) or diagonal line and requires at least one free position on an inner ring in the direction of the move.
- A piece is captured when it is squeezed between two opponent pieces.
- A player wins by conquering the throne at the center or by capturing all of the opponent pieces.

## Running locally

The project ships compiled jars under `src/Morelli_v0.1.1/dist/` (the game client) and `src/Morelli_v0.1.1/netgames/` (the NetGames server). To play a local match you start the server first and then two game clients.

```
git clone https://github.com/nicolasfvp/morelli-boardgame.git
cd morelli-boardgame/src/Morelli_v0.1.1
```

Start the NetGames server:

```
java -jar netgames/servidor.jar
```

Then start the Morelli client. Run it twice, once for each player:

```
java -jar dist/Morelli.jar
```

The server reads its configuration from `server.properties`. The default listen host is `localhost` and the default port is 1099, so the server and both clients run on the same machine unless the properties are changed.

If you prefer to build from source, the project uses the NetBeans Ant build defined in `src/Morelli_v0.1.1/build.xml`:

```
cd src/Morelli_v0.1.1
ant
```

## Project structure

- `src/Morelli_v0.1.1/src/` Java sources, organized into `morelli` (entry point), `entidades` (board, pieces, moves and game entities), `interfaceGrafica` (Swing screens and player actor) and `mensagens` (localized message bundles).
- `src/Morelli_v0.1.1/dist/` prebuilt game client jar and its runtime libraries.
- `src/Morelli_v0.1.1/netgames/` NetGames server jar and configuration.
- `relatorio/` academic report (`relatorio.pdf`) and annexes describing the maintenance work.
- `uml/` class, sequence and layer diagrams.
- `logs/` sample execution logs.

## Documentation

A written report is available at `relatorio/relatorio.pdf`, with supporting annexes under `relatorio/`. The annexes document findings from the maintenance work, including dead and duplicated code identified in the legacy sources.

## Status

Academic project. It is a maintenance exercise on a legacy codebase, so parts of the source and inline comments are in Portuguese.

## License

Released under the MIT License. See the LICENSE file for details.
