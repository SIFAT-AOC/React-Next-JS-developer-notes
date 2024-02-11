### Separating Event From Effects
1.Event handlers run in response to specific interactions.
2.Effects run whenever synchronization is needed.
3.Logic inside event handlers is not reactive.
4.Logic inside Effects is reactive.
5.You can move non-reactive logic from Effects into Effect Events.
6.Only call Effect Events from inside Effects.
7.Don’t pass Effect Events to other components or Hooks.


### Effect Events are very limited in how you can use them:

1 .Only call them from inside Effects. /
2 .Never pass them to other components or Hooks.
