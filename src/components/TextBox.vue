<template>
    <div class="main">
        <div class='text-input' ><span class="correct-text">{{correctText}}</span>{{snippet}}</div>
        <input placeholder="Type Here" v-model="userInput">
    </div>
</template>

<script>
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
        isInputDisabled: false
    }
  },
    watch: {
        userInput: function (val) {
            if(val.length < 1) return;
            // TODO: handle backspace
            // TODO: indicate to user where typed text is incorrect
            if (val[val.length - 1] === this.snippet[0]) {
                this.correctText = val;
                this.snippet = this.snippet.slice(1, this.snippet.length);
            }
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

    .text-input {
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
</style>
