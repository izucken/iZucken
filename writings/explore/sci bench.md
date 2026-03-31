I am creating a game. What do you thing it is for?

This game is designed to be playable by human and AI.

It is played via API.

In this game you get to control a META PROBE. With it you can explore an ABSTRACT UNIVERSE. You can read the MANUAL. You get 1 terawatt of budget. You can submit COMMUNICATION by paying watts. You can FINISH the game at any point to get INDEPENDENT TRIAL. The goal of this game is to BUILD A MODEL of the given universe. You win a round with perfect 100% score if your MODEL is 100% predicts every TRIAL. You get 50% score if your MODEL is 99.9% accurate. You get 10% score if your MODEL is 99% accurate, and zero otherwise. You can play infinitely. Each round you get a RANDOMISED universe with randomised laws. Your PROBE MANIPULATORS and SENSORS are also randomised. COMMUNICATION with a probe has limited BANDWIDTH. You pay watts per spent BANDWIDTH per COMMUNICATION ROUNDTRIP. In the MANUAL you can read what manipulators and sensors you have what data kind of they receive and send, and how they receive and send data. More complicated apparatus requires more bandwidth. The PROTOCOL is always textual like:

```
X: 1
Y: 1
A?
---
A: NaN
```

Bandwidth is guaranteed to fit at least the largest datapoint. You must not assume anything about the explored universe. You submit your MODEL OF THE UNIVERSE as a program that computes sensor values from manipulator values - prediction program. You have only one try per round (per game) and you can never retry the same universe again (except by chance). All universes and probes are random every game for every player. How the player arrives at the model is fully up to the player.

EXAMPLE GAME 1:

MANUAL (simplified):
You have BOOLEAN manipulator X
You have BOOLEAN sensor A

MODEL:

```js
function model(x) { return {a: x}; }
```

So in this example it is AN BOOLEAN IDENTITY UNIVERSE.

EXAMPLE GAME 2:

MANUAL (simplified):
You have BOOLEAN manipulator X
You have BOOLEAN sensor A

MODEL:

```js
function model(x) { return {a: !x}; }
```

So in this example it is AN BOOLEAN NOT UNIVERSE.

EXAMPLE GAME 3:

MANUAL (simplified):
You have REAL manipulator BEAR
You have REAL manipulator CAT
You have REAL manipulator DOG
You have INTEGER sensor FUNNY
You have INTEGER sensor PATHETIC
You have INTEGER sensor AWESOME

MODEL:

```js
function model(bear, cat, dog) {
  return {
    funny: floor(dog)
    pathetic: floor(cat)
    awesome: floor(bear)
  };
}
```

So in this example it is a sort of discrete 3D positioning universe.
