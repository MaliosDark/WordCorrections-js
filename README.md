## WordCorrections.js

WordCorrections.js is a JavaScript file designed to clean responses received from the Serge Chat API by correcting words with spaces. It provides a simple solution to enhance text processing and improve the accuracy of word interpretations.

## Usage

To integrate WordCorrections.js into your project, include the following script tag in your HTML file:

```markdown
<script src="https://cdn.jsdelivr.net/gh/MaliosDark/WordCorrections-js/wordCorrections.js"></script>
```

After including the script, you can utilize the `applyWordCorrections` function in your JavaScript code to apply corrections to a given text.

```javascript
const cleanedText = applyWordCorrections("Your text with spaces");
console.log(cleanedText);
```

Additionally, you may use the `cleanResponse` function to clean responses received from the Serge Chat API. Here's an example of how it can be used:

```javascript
function cleanResponse(data) {
    let cleanData = data.replace(/data:|event: message|event: close/g, '');
    const removePing = cleanData.replace(/: ping - \d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2}.\d{6}/g, '');
    const trimmedData = removePing.replace(/\s+/g, ' ').trim();
    const removeInstructions = trimmedData.replace(/##\s?#\s?Instruction\s?:[^#]+/g, '').replace(/##\s?#\s?Response\s?:[^#]+/g, '');
    let cleanContent = removeInstructions.replace(/##\s?#\s?[^#]+:\s?[^#]+/g, '').trim();

    // New code to handle words with spaces
    const wordsWithSpaces = cleanContent.match(/"([^"]+)":"([^"]+)"/g);
    if (wordsWithSpaces) {
        wordsWithSpaces.forEach(wordPair => {
            const [original, replacement] = wordPair.split('":"');
            cleanContent = cleanContent.replace(new RegExp(original, 'g'), replacement);
        });
    }

    // Apply word corrections
    cleanContent = applyWordCorrections(cleanContent);

    return cleanContent;
}
```

## Motivation

WordCorrections.js emerged as a targeted solution to address a specific challenge posed by responses from the Serge Chat API. Focusing on words with spaces, the primary objective is to elevate the general quality of text interpretation, response formulation, and overall comprehension. This library strives to contribute to a more refined and accurate understanding of textual content, particularly in scenarios where word corrections play a crucial role in optimizing communication and interpretation.

## Contributing

If you wish to contribute to WordCorrections.js, we welcome you to fork the repository and submit a pull request. Please adhere to best coding practices and maintain code cleanliness.

## Issues

If you encounter any issues or have suggestions, feel free to open an issue on the [GitHub Issues](https://github.com/MaliosDark/WordCorrections-js/issues) page.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```
