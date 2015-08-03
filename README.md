# yarn-media-queries
Set application-wide media queries so many elements can be responsive without each maintaining an independent list of queries.

## How it Works
-The `yarn-media-queries` element maintains a list of media queries.
-The last element in the list that matches is the winner.
-The winning media type is stored in application state via yarn-state-behavior.
-`yarn-media-query-behavior` applies the winning media type as a class on the host element.

## Include the element once
Use the `yarn-media-queries` element *once* in your application.  e.g.
```
<link rel="import" href="../bower_components/yarn-media-queries/yarn-media-queries.html">
<my-app>
  <yarn-media-queries></yarn-media-queries>
  <responsive-element-one></responsive-element-one>
  <responsive-element-two></responsive-element-two>
</my-app>
```
## Responsive elements include the behavior
The behavior applies the winning media type to the host as a class.
```
<dom-module id="responsive-element-one">
  <style>

    h1{
      font-size: 3em;
    }

    :host.medium-screen h1{
      font-size: 2em;
    }

    :host.small-screen h1{
      font-size: 1em;
    }

  </style>

  <template>
    <h1>Responsively Sized Header</h1>
  </template>

</dom-module>
<script>
  (function () {
    Polymer({
      is: 'responsive-element-one',
      behaviors: [YarnBehaviors.MediaQueryBehavior]
    });
  })();
</script>
```
## Default queries
These are the defaults and work without additional configuration:
```
this.queries = [
  {
    query: '(min-width: 0px)',
    class: 'small-screen',
  },
  {
    query: '(min-width: 500px)',
    class: 'medium-screen'
  },
  {
    query: '(min-width: 1000px)',
    class: 'large-screen'
  },
  {
    query: '(min-width: 1000px) and (max-height: 1000px)',
    class: 'laptop-screen'
  }
];
```
## Custom queries
Change the list and detail of queries at the application level to suit your needs.
```
<dom-module id="my-app">

  <template>
    <yarn-media-queries queries="{{queries}}"></yarn-media-queries>
    <responsive-element-one></responsive-element-one>
    <responsive-element-two></responsive-element-two>
  </template>

</dom-module>
<script>
  (function () {
    Polymer({
      is: 'my-app',
      behaviors: [YarnBehaviors.MediaQueryBehavior],
      ready: function(){
        var queries = [
          {
            query: '(min-width: 0px)',
            class: 'small-screen',
          },
          {
            query: '(min-width: 400px)',
            class: 'medium-screen'
          },
          {
            query: '(min-width: 1200px)',
            class: 'large-screen'
          }
        ];
        this.set('queries', queries);
      }
    });
  })();
</script>
```
