<template>
  <div class="body">
  <div class="main">
    <div class="img-container">
      <img :src="selectedItem.img" alt="Selected Image" />
      <div class="special">
        <div v-show="selectedItem.special" class="special-alert">-{{ selectedItem.special }}%</div>
        <div v-show="selectedCable != cables[0]" class="special-alert special-alert__warn">!</div>
      </div>
    </div>
    <section class="desc">
      <span class="desc-theme">headphones</span>
      <h1 class="desc-header">Beats EP</h1>
      <div class="desc-option">
        <p class="desc-option__text">Lorem Ipsum is simply dummy text of the printing and typesetting industry.
          Lorem Ipsum has been the industry's standard dummy text ever since the 1500s,
          when an unknown printer took a galley of type and scrambled it to make a type specimen
          book. It has survived not only five centuries, but also the leap into electronic
          typesetting, remaining essentially unchanged.
        </p>
        <hr>
        <div class="desc-option__item">
          <span>Color</span>
          <div class="buttons-inline">
            <button class="button-color" @click="changeColor(item)" v-for="item in items" :key="item.color"
              :style="{ 'background-color': item.color }">{{ item.label === selectedItem.label ? '✓':'' }}</button>
          </div>
        </div>
        <div class="desc-option__item">
          <span>Cable configuration</span>
          <div class="buttons-inline">
            <button class="button-cable" :class="{ active: selectedCable === cable }" @click="choseCabel(cable)"
              v-for="cable in cables" :key="cable">{{ cable }}</button>
          </div>
        </div>
        <div class="desc-help">
          <div class="desc-help-icon">?</div>
          <span>How to configurate your headphones</span>
        </div>
        <hr />
        <div class="desc-submit">
          <div class="price">{{ price }}$</div>
          <button class="button-submit" @click="confirm()">Add to cart</button>
        </div>
      </div>
    </section>
  </div>
  </div>
</template>

<script setup lang="ts">
interface itemData {
  img: string,
  color: string,
  label: string,
  special: number,
}

const items: itemData[] = [{
  img: "/images/blackImg.webp",
  color: 'black',
  label: 'black',
  special: 0,

}, {
  img: "/images/redImg.webp",
  color: '#a83534',
  label: "red",
  special: 5,
}, {
  img: "/images/whiteImg.webp",
  color: '#d6dbdf',
  label: 'white',
  special: 10,
}]

const selectedItem = ref<itemData>(items[0]);

const defPrice = 148;
const price = ref<number>(defPrice);

const changeColor = (item: itemData): void => {
  selectedItem.value = item;
  price.value = defPrice / 100 * (100 - item.special);
};

const cables: string[] = ['Straight', 'Coiled', 'Long-coiled'];
const selectedCable = ref<string>(cables[0]);

const choseCabel = (cabel: string): void => {
  selectedCable.value = cabel;
};

const confirm = (): void => {
  alert('Поздравляю с покупкой!');
}
</script>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-weight: lighter;
}

.body{
  font-family: 'Raleway', sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
}

.main {
  display: grid;
  grid-template-columns: 2fr 1fr;
  justify-content: center;
  gap: 5px;
  max-width: 75vw;
  background-color: #f7f7f7;
}

.img-container {
  position: relative;
}

img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}

.desc {
  display: flex;
  flex-direction: column;
  row-gap: 30px;
  padding: 20px;
}

.desc-theme {
  color: #6ba0dc;
  text-transform: uppercase;
  cursor: pointer;
  font-size: 14px;
}

.desc-header{
  font-size: 42px;
  color: #5d5e60;
}

.desc-option {
  display: flex;
  flex-direction: column;
  gap: 20px;
  color: #858585;

}

.desc-option__item {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.desc-option__item > span {
  font-weight: bold;
}

.buttons-inline {
  display: flex;
  gap: 5px;
}

.desc-help {
  display: flex;
  align-items: center;
  gap: 5px;
  color: #6ba0dc;
  cursor: pointer;
}

.desc-help-icon {
  position: relative;
  padding: 0 5px;
  color: #6b95b7;
}

.desc-help-icon {
  color: #b6ccdf;
}
.desc-help-icon::after {
  content: "";
  position: absolute;
  top: 0;
  left: 1px;
  width: 15px;
  height: 15px;
  border-radius: 100%;
  border: 1px solid #b6ccdf;
}

.desc-submit {
  display: flex;
  column-gap: 20px;
  align-items: center;
  justify-content: flex-start;
}

.price {
  font-size: 24px;
  min-width: 80px;
}

button {
  cursor: pointer;
}

.button-cable {
  padding: 10px 15px;
  border: 2px solid gainsboro;
  border-radius: 4px;
  background-color: transparent;
}

.button-cable:hover {
  border-color: #8dc860;
}

.button-cable.active {
  border: none;
  background-color: #8dc860;
  color: white;
}

.button-color {
  border-radius: 100%;
  border: none;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  font-size: 36px;
  color: white;
  outline: 2px solid white;
}

.button-color:hover {
  outline-color: #8dc860;
}

.button-submit {
  padding: 15px;
  border: none;
  border-radius: 12px;
  background-color: #8dc860;
  color: white;
  font-weight: bold;
}

.special {
  position: absolute;
  right: 0;
  top: 0;
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.special-alert {
  width: 100px;
  height: 100px;
  color: #ea4125;
  border: 3px #ea4125 solid;
  border-radius: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 28px;
}

.special-alert__warn {
  background-color: #ea4125;
  color: white;
  font-size: 48px;
}

</style>
