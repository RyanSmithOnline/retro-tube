<template>
  <div>
    <input id="input" />
    <iframe id="video" style="display:none" width="560" height="315" src="" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    <div id="images">
      <span id="loading">LOADING...</span>
    </div>
  </div>

</template>


<script>
let getVideoList = async () => {
return await fetch('https://youtube.googleapis.com/youtube/v3/search?part=snippet&publishedBefore=2008-01-01T00%3A00%3A00Z&q=ryan&key=AIzaSyD20G9Qrqk3KFPoP9W1OjORKi1emECAAYE&max-results=5')
  .then(response => response.json());
};
Promise.resolve(getVideoList()).then(data => {
  data.items.forEach((element, index) => {
      let newElement = document.createElement('img');
      let button = document.createElement('button');
      let video = document.getElementById('video');
      newElement.src = element.snippet.thumbnails.default.url;
      button.onclick(()=>{
        video.src = 'https://www.youtube.com/embed/' + element.id.videoId;
        video.style.display = 'block';
      })
      document.getElementById('images').append(newElement);
      document.getElementById('images').append(button);
      if(data.items.length == index + 1){
        document.getElementById('loading').remove();
      }
  });
  console.log(data);
});
export default {
  name: 'RetroTube',
}
</script>
