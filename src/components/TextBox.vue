<template>
    <div class="main">
        <textarea class='text-input' disabled="true" v-model="snippet"></textarea>
        <input @input="eventText" placeholder="Type Here" v-model="userInput">
    </div>
</template>

<script>
// TODO: Put code files in static folder structure and import as string
const snippet = 'const storage = require(\'../storage\');\n' +
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
        snippet,
        userInput: '',
        isInputDisabled: false
    }
  },
    watch: {
        userInput: function (val) {
            if (this.userInput[val.length - 1] !== snippet[val.length - 1]) {
                console.log(false)
            } else {
                console.log(true)
            }
        }
    },
    methods: {
        eventText(event) {
            console.log(event)
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
    font-family: droid,sans-serif;
      font-size: 18px;
  }
</style>
