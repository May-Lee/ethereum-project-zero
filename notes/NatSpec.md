# Understanding NatSpec 
###### (from [Solidity Documentation](https://docs.soliditylang.org/en/latest/natspec-format.html))

Ethereum Natural Language Specification Format

- Inspired by [Doxygen](https://en.wikipedia.org/wiki/Doxygen)

Solidity contracts SHOULD be fully annotated using NatSpec for all public interfaces (everything in the ABI)

Documentation (i.e., comments) MUST be inserted above each of the following, using the Doxygen notation format:

- `contract`
- `interface`
- `function`
- `event`
- `public` state variables are EQUIVALENT to `function` for the purposes of NatSpec

In Solidity, use:

- `///` for single or multi-line comments
- or `/**` ending with `*/`

Documentation output from the comments is segmented into developer-facing messages and end-user-facing messages.

- The Solidity compiler exracts these comments into a machine-readable format
- These messages then may  be shown to the human at the time a Tx is signed

NOTE: Solidity has no intention to keep strict compatibility with Doxygen

## Tags

Tags are optional.

In the absence of tags, the Solidity compiler interprests `///` or `/**` as if tagged with `@notice`

Use multiple `@param` or `@return` statements in the case of multiple return values and parameters.

| Tag           | Description                                                                        | `contract` | `library` | `interface` | `function`  | `public` state variable | `event` |
|---------------|------------------------------------------------------------------------------------|:----------:|:---------:|:-----------:|:-----------:|:-----------------------:|:-------:|
| `@title`      | A title should describe the contract/interface                                     |      *     |     *     |      *      |             |                         |         |
| `@author`     | The name of the author                                                             |      *     |     *     |      *      |             |                         |         |
| `@notice`     | Explain to an end user what this does                                              |      *     |     *     |      *      |      *      |            *            |    *    |
| `@dev`        | Explain to a developer any extra details                                           |      *     |     *     |      *      |      *      |            *            |    *    |
| `@param`      | Documents a parameter and must be followed by parameter name                       |            |           |             |      *      |                         |    *    |
| `@return`     | Documents the return variables of a contract's function                            |            |           |             |      *      |            *            |         |
| `@inheritdoc` | Copies all missing tags from base function (must be followed by the contract name) |            |           |             |      *      |            *            |    *    |
| `@custom:`    | Custom tag, semantics is application-defined (see below)                           |      *     |     *     |      *      |      *      |            *            |    *    |

### Custom tags

Annotations used by third-party tools can be accomplished using `@custom:`

- MUST be followed by one or more lowercase letters or hyphens
- CAN NOT start with a hyphen
- CAN be used everywhere and are part of the developer documentation 
- A possible use case of this tag is analysis and verification tools

## Inheritance

Functions without NatSpec will automatically inherit the documentation of their base function, EXCEPT:

- When the parameter names are different
- When there is more than one base function
- When there is an explicit `@inheritdoc` tag

## Output

Generate documentation using 

`solc --userdoc --devdoc ex1.sol`

Before Solidity 0.6.11, the documentation would produce two different JSON files: one for the end user as a notice when a function is executed and the other by the developer.

After Solidity 0.6.11, the output will also contain a `version` and a `kind` field. `version` is set to `1` but it is possible new versions might be introduced. `kind` must be EITHER `user` or `dev`

What is the output of the contract here:

<Link to contract> 

Note that the key by which to find the methods is the function's canonical signature as defined in the [Contract ABI](https://docs.soliditylang.org/en/latest/abi-spec.html#abi-function-selector) and not the function's name.

## Other

Dynamic expressions: end-user client software may present JSON directly or apply pre-processing. Specifying dynamic expressions is outside of the scope of the Solidity documentation and more can be read here: https://github.com/aragon/radspec

At the time of this writing, the Solidity compiler only interprets tags if they are external or public. Comments used in internal and private functions will not be parsed.
