| Mode             | Description                                                                                            |
|------------------|--------------------------------------------------------------------------------------------------------|
| `random`         | Select a random element each time. *(default)*                                                         |
| `one`            | Select the same, random element each time.                                                             |
| `forward`        | Select in a wrapping sequence from first to last.                                                      |
| `forward-clamp`  | Select from first to last, then repeat the last element forever.                                       |
| `forward-mirror` | Select from first to last, then last to first, then start over.                                        |
| `reverse`        | Select in a wrapping reverse sequence from last to first.                                              |
| `reverse-clamp`  | Select from last to first, then repeat the first element forever.                                      |
| `reverse-mirror` | Select in a from last to first, then first to last, then start over.                                   |
| `deck`           | Select each element once in a random sequence, then reshuffles.                                        |
| `deck-loop`      | Select each element once in a wrapping random sequence, without reshuffling.                           |
| `deck-clamp`     | Select each element once in a random sequence, repeating the final element.                            |
| `deck-mirror`    | Select each element once in a random sequence, then repeats the sequence backwards before reshuffling. |
| `ping`           | Select from first to last, switching directions when a boundary element is reached.                    |
| `pong`           | Select from last to first, switching directions when a boundary element is reached.                    |
| `no-double`      | Select a random element each time, ensuring the same element never occurs twice in a row.              |