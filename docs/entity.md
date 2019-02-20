# Entity

Intents have metadata about the intent called “Entities”. Let’s take an example for an Intent 

“BookAFlight”  --> Sample Utterance: “I want to book a flight to Vancouver”

Some entities may be labelled as composite entities that is having more than one entities (component entity) inside it. As a science, it doesn’t matter if you don’t have this feature with your NLP service as long as you have simple entity labelling. One must define component entities before labelling composite entities. 

More examples:- Find me a pair of Size **8** **_Red_** **Adidas** **_Sport shoes_**.

Intent —> SearchProduct

Entities —>
  - Size — 8
  - Brand — Adidas
  - color — Red
  - Category — Sport Shoes

<iframe width="500" height="270" src="https://www.youtube.com/embed/kzdL6GxJ_WY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>