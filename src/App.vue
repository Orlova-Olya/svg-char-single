<template>
  <div id="app">
    <table>
      <tbody>
        <tr>
          <td>
            <label for="sideLength">sideLength:</label>
          </td>
          <td>
            <input v-model="sideLength" id="sideLength" type="number" min="0" />
          </td>
        </tr>
        <tr>
          <td>
            <label>ringWidth:</label>
          </td>
          <td>
            <input v-model="ringWidth" type="number" min="0" />
          </td>
        </tr>
        <tr>
          <td>
            <label for="ringColor">ringColor:</label>
          </td>
          <td>
            <input v-model="ringColor" id="ringColor" type="color" />
          </td>
        </tr>
        <tr>
          <td>
            <label for="arcWidth">arcWidth:</label>
          </td>
          <td>
            <input v-model="arcWidth" id="arcWidth" type="number" min="0" />
          </td>
        </tr>
        <tr>
          <td>
            <label for="arcColor">arcColor:</label>
          </td>
          <td>
            <input v-model="arcColor" id="arcColor" type="color" />
          </td>
        </tr>
        <tr>
          <td>arcStrokeLinecap:</td>
          <td>
            <label>
              <input v-model="arcStrokeLinecap" type="radio" value="butt" />
              butt
            </label>
            <label>
              <input v-model="arcStrokeLinecap" type="radio" value="square" />
              square
            </label>
            <label>
              <input v-model="arcStrokeLinecap" type="radio" value="round" />
              round
            </label>
          </td>
        </tr>
        <tr>
          <td>
            <label for="percentage">percentage:</label>
          </td>
          <td>
            <input v-model="percentage" id="percentage" type="number" max="100" min="0" />
          </td>
        </tr>
      </tbody>
    </table>

    <Char
      :percentage="+percentage"
      :sideLength="+sideLength"
      :ringWidth="+ringWidth"
      :ringColor="ringColor"
      :arcWidth="+arcWidth"
      :arcColor="arcColor"
      :arcStrokeLinecap="arcStrokeLinecap"
    />
  </div>
</template>

<script>
import Char from './components/Char.vue'

export default {
  id: 'App',
  components: { Char },

  data: () => ({
    percentage: 25,
    sideLength: 100,
    ringWidth: 20,
    ringColor: '#e0e0e0',
    arcWidth: 20,
    arcColor: '#fea948',
    arcStrokeLinecap: 'butt'
  })
}
</script>

<style lang="scss">
html,
body {
  min-height: 100%;
  display: flex;
  flex-direction: column;
}
body {
  flex-grow: 1;
  margin: 0;
  display: flex;
  flex-direction: column;
}
#app {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

table {
  margin-bottom: 16px;
  font-size: 20px;
}
td {
  width: 50%;
}
td:first-child {
  text-align: right;
  padding: 8px 8px 8px 0;
}
input[type='number'],
input[type='color'] {
  font-size: 16px;
  width: 100px;
  box-sizing: border-box;
}
label:not(:only-child) {
  display: block;
}
</style>
