<template>
  <textarea class='text-input' v-model="text"></textarea>
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
        '};\n'

export default {
  name: 'TextBox',
  props: {
    msg: String
  },
  data() {
    return {
      text: snippet

    }
  }
}
</script>

<style scoped>
  .text-input {
    height: 500px;
    width: 100%;
    background: grey;
    color: white;
    border: none;
    padding: 10px 10px 0;
    font-family: droid,sans-serif;
    font-size: 32px;
  }
</style>
