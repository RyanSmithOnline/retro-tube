<template>
  <div>
    <input id="input" />
    <div id="images">
      <span id="loading">LOADING...</span>
    </div>
  </div>
</template>

<script>
let getVideoList = async () => {
return await fetch('https://youtube.googleapis.com/youtube/v3/search?part=snippet&publishedBefore=2008-01-01T00%3A00%3A00Z&q=a&key=AIzaSyD20G9Qrqk3KFPoP9W1OjORKi1emECAAYE')
  .then(response => response.json());
};
Promise.resolve(getVideoList()).then(data => {
  console.log(data.items.length);
  data.items.forEach((element, index) => {
    console.log(index);
    //setTimeout(() => {
      let newElement = document.createElement('img');
      newElement.src = element.snippet.thumbnails.default.url;
      document.getElementById('images').append(newElement);
      if(data.items.length == index + 1){
        document.getElementById('loading').remove();
      }
    //}, index * 1000);
  });
  console.log(data);
});
export default {
  name: 'RetroTube',
}
</script>
