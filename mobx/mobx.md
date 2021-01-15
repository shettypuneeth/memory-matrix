# State management with mobx

Built around four core concepts

1. Computed value
2. Reactions
3. Observable state
4. Actions

## Computed Values

> Find the smallest amount of state you need and derive all the other relevant things

We mark the derivations with @computed.

- Informs mobx that these values can be derived from other observables.
- Computed values are not allowed to produce side effects, like changing state or making network requests.
- Computations are triggered when we assign the value to the observable, rather they are triggered when we inspect the value.
- Mobx does not keep the value of the computed value up to date.
- Mobx defers the computations till the value is invoked via i/o or side effects.

## Reactions

We leant that mobx defers the computations on observed value till it's invoked. But if we want to make it reactive, we need to wrap them in a _reactions_

Reactions don't produce a value, but instead they produce a side effect.

`Observer` is an example of a reaction. And side effect of the observer decorator is that it flushes a rendering to the DOM.

> Computed expressions have to be side effect free cause mobx decides when it's a good moment to re-evaluate those expressions.
> This allows mobx to have millions of computed properties in memory but only actively track few of them, those that are directly or indirectly used by some reaction.

## Observable

Using the `observable` function we can make an object observable. It enumerates the properties and creates an observable property for each key value pair.
If we pass function as value then mobx creates a computed value

```js
const Temperature = observable({
  unit: "C",
  temperatureCelsius: 25,
  temperatureKelvin: function () {
    return this.temperatureCelsius + 273.15;
  },
  temperatureFahrenheit: function () {
    return this.temperatureCelsius * (9 / 5) + 32;
  },
  temperature: function () {
    switch (this.unit) {
    }
  },
});
```

## Actions

Any code that tries to alter the state is an action. We use @action decorator to indicate that the functions is an actions and can change state.

- Actions modify state, which inturn triggers reactions. This completes the loop of state management

Mobx runs all derivations synchronously. That means if you make two modifications, mobx runs the base computations twice.

But you can club them using `transactions`

```js
transaction(() => {
  Temperature.unit = "F";
  Temperature.unit = "C";
});
```

When you use actions, they automatically apply transactions.
