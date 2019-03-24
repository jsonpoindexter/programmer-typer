<template>
    <div class="main">
        <div class='snippet'><span class="correct-text">{{correctText}}</span>{{snippet}}</div>
        <textarea class='user-input' placeholder="Type Here" v-model="userInput"/>
    </div>
</template>

<script>
    // Top text box should contain correct text to be typed
    // Bottom box should be text input to show text being typed and incorrect text being types (red)
    // Top text should change background color to green as it is correctly types in the bttom

    // TODO: Put code files in static folder structure and import as string
    let snippet = 'const storage = require(\'../storage\');\n' +
        '\n' +
        'module.exports = async (req, res) => {\n' +
        '    try {\n' +
        '        const meta = await storage.metadata(req.params.id);\n' +
        '        res.set(\'WWW-Authenticate\', `send-v1 ${meta.nonce}`);\n' +
        '        res.send({\n' +
        '            requiresPassword: meta.pwd\n' +
        '        });\n' +
        '    } catch (e) {\n' +
        '        res.sendStatus(404);\n' +
        '    }\n' +
        '};\n';

    export default {
        name: 'TextBox',
        props: {},
        data() {
            return {
                snippet: snippet,
                userInput: '',
                correctText: '',
                isInputDisabled: false,
                isLastCharWrong: false,
                index: 0,
            }
        },
        watch: {
            userInput: function (val) {
                if (val.length < 1) return;
                if (val[this.index] === this.snippet[0]) {
                    this.correctText = val;
                    this.snippet = this.snippet.slice(1, this.snippet.length);
                    this.index++
                }
                console.log(this.snippet)
            }
        }
    }
</script>

<style scoped>
    .main {
        margin-top: 100px;
        display: flex;
        flex-direction: column;
        height: 200px;
        width: 600px;
    }

    .snippet {
        background: black;
        height: 100%;
        color: white;
        border: none;
        padding: 10px 10px 0;
        font-family: droid, sans-serif;
        font-size: 18px;
        white-space: pre-wrap;
        overflow-y: auto;
    }

    .correct-text {
        background-color: lightgreen;
    }

    .user-input {
        resize: none;
    }


</style>
