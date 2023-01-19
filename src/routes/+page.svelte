<script>
  let clicks = 0;
  let multiplier = 1;
  let workers = [];
  let worker_multiplier = 1;

  let upgrades = [
    { cost: 100, name: "5% increase", multiplier: 1.05, worker: 0 },
    { cost: 250, name: "Printer", multiplier: 0, worker: 1 },
  ];

  function increment() {
    clicks = clicks + multiplier;
    var audio = new Audio('money.mp3');
audio.play();
    console.log("click" + clicks);
  }
</script>

<article>
  <header>
    <div class="grid">
      {#each upgrades as upgrade}
        <button
          class="upgrade"
          on:click={() => {
            if (clicks >= upgrade.cost) {
              if (upgrade.multiplier) {
                multiplier = multiplier * upgrade.multiplier;
                clicks -= upgrade.cost;
              }
              if (upgrade.worker && clicks) {
                worker_multiplier = worker_multiplier * 1.5;
                workers = [upgrade.name, ...workers];
                /* start "clicking" every 5000 ms */
                setInterval(increment, 5000);
                clicks -= upgrade.cost;
                upgrade.cost = upgrade.cost * worker_multiplier;
              }
            } else {
              alert("Insufficient funds! Earn more!");
            }
          }}
        >
          <span>{upgrade.name}</span>
          <span>${upgrade.cost}</span>
        </button>
      {/each}
    </div>
  </header>
  <div class="game">
    <button on:click={increment} class="clicker">
      <span class="clicks">${clicks.toFixed(2)}</span>
      <span class="pointtext">M.P.C: {multiplier.toFixed(2)}</span>
    </button>
  </div>
  <footer>
    <div class="panelright">
      <div>
        <span>-|Tools & Assistance|-</span>
        <hr />
        <div class="shop">
          {#each workers as worker}
            <div class="worker">{worker}</div>
          {/each}
        </div>
      </div>
      <hr />
    </div>
  </footer>
</article>

<style>
  .shop {
    display: grid;
    grid-auto-flow: row; /* default */
    gap: 8px;
    grid-template-rows: repeat(3, 1fr);
    grid-template-columns: repeat(3, 1fr);
  }

  .upgrade {
    width: 100%;
    height: 100%;
    color: rgb(255, 242, 0);
    border: 4px solid rgb(219, 16, 16);
    background-color: rgb(59, 183, 28);
    background-size: cover;
    background-image: url("https://xtrastoragecompaniesfl.com/wp-content/uploads/2018/06/66095332_l-1080x675.jpg");
    place-items: center;
    place-content: center;
    display: flex;
    flex-direction: column;
  }

  .worker {
    width: 100%;
    height: 100%;
    border: 1px solid black;
    background-color: rgb(27, 141, 120);
    background-size: cover;
    background-image: url("https://xtrastoragecompaniesfl.com/wp-content/uploads/2018/06/66095332_l-1080x675.jpg");
    place-items: center;
    place-content: center;
    display: flex;
  }

  .game {
    height: 50vh;
    display: flex;
    flex-direction: column;
    place-items: center;
    background-image: url("https://thumbs.gfycat.com/EuphoricIcyAmericanshorthair-size_restricted.gif");
    background-size: cover;
    background-position: 0px -200px;
    place-content: center;
  }
  .clicker {
    clip-path: circle();
    display: flex;
    height: 100%;
    width: 100%;
    flex-direction: column;
    place-items: center;
    place-content: center;
    background-image: url("https://www.marxist.com/images/stories/economy/Money_-_Pictures_of_Money--Flickr_flickr.com--photos--pictures-of-money--17123251389.jpg");
    background-size: cover;
    background-position: 0px -200px;
  }

  .panelright {
    height: 100%;
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .clicks {
    color: rgb(0, 0, 0);
    font-size: 100px;
  }

  .pointtext {
    color: rgb(7, 48, 26);
    font-size: 25px;
    font-weight: bold;
  }
</style>
