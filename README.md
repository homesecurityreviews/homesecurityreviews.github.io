<!-- todo
-Card specific scoping for elipses show more
- add show more
- data entry blue object
- clean up vue.js data object
- update rating on dropdown change
- dropdown to see what items are selected for compare
- create modal experience
- move to index
- design short cards
- update number rankings
- implement mobile
- show cards on compare button roll over
- update card criteria based on selection
-create fancier v-cloak loading...
 -->
<!DOCTYPE html>
<html>
<head>
  <!-- Standard Meta -->
  <meta charset="utf-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="viewport" content="width=device-width, initiaPGl-scale=1.0, maximum-scale=1.0">

  <!-- Site Properties -->
  <title>Home Security Reviews</title>
  <link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.3.1/semantic.css">
  
  <link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.3.1/components/dropdown.css">
  <link rel="stylesheet" type="text/css" href="/assets/library/global.css">

  <style type="text/css">
  </style>


  <script
  src="https://code.jquery.com/jquery-3.3.1.min.js"
  integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="
  crossorigin="anonymous"></script>
  <script src="http://cdn.jsdelivr.net/jquery.glide/1.0.6/jquery.glide.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.3.1/components/dropdown.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.3.1/semantic.js"></script>
<script src="https://cdn.jsdelivr.net/npm/js-cookie@2.2.0/src/js.cookie.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/axios/0.15.2/axios.min.js" type="text/javascript"></script>
<script src="https://unpkg.com/vue@2.2.5/dist/vue.js" type="text/javascript"></script>

  <script src="../assets/library/blue.js"></script>
  <script src="../assets/library/data.js"></script>
  <script>
    $(document)
      .ready(function() {
        // create sidebar and attach to menu open
        $('.ui.sidebar')
          .sidebar('attach events', '.toc.item')
        ;
      })
    ;
  </script>
  <script>
    $(document)
      .ready(function() {
        // $('.special.card .image').dimmer({
        //   on: 'hover'
        // });
        $('.star.rating')
          .rating()
        ;
        // $('.card .dimmer')
        //   .dimmer({
        //     on: 'hover'
        //   })
        // ;
      })
    ;
  </script>
</head>
<body>
<div id="app" v-cloak >

<div class="ui vertical masthead center aligned segment">
        <h1 class="ui active item" style="font-size:1em;" vt-once ><strong>{{appName}}</strong></h1>
        
    </div>
</div>


<script type="text/javascript">
var app = new Vue ({
    el: '#app',
    data: {
      compareNag:true,
      banner:"Editor's Choice",
      rankby:"editor",
      cardTitle:"nickname",
      line1:["","description"],
      line2:["Basic Pricing:","basicPricing"],
      line3:["Advanced Pricing:","advancedPricing"],
      blue: blue,
      isActive:false,
      isTruncate:true,
      compare:compareCookie,
      rank:["frontPoint","pro1","vivint","adt","cpi","brinks","protectAmerica","simpliSafe","ackerman","csg"],
      appName: "Home Security Reviews",
      nav:{
        itemOne: {
          name:'Top Ranked',
          link:'#'
        },
        itemTwo: {
          name:'Find Your Best Match',
          link:'#'
        },
        itemThree:{
          name: 'All Systems',
          link:'/best-home-security/'
        }
      },
      headline:{
        msg1:'Trust facts, not salespeople.',
        msg2: ''
      }
    },
    methods:{
       toggleCompare: function (name){
          var pos = this.compare.indexOf(name);
          if (pos == -1){
            this.compare.push(name);
            Cookies.set('compare', app.compare.join(), { expires: 365 });
          }else {
            this.compare.splice(pos,1);
            Cookies.set('compare', app.compare.join(), { expires: 365 });
          if ( app.compare.length == 0){
            app.compareNag = true;};
          };
          $(".dimmable").dimmer("hide");
          app.compare.map(function(sys){
            $("."+sys).dimmer("show");
          });
        },
      truncate: function (value,boo) {
      if (!value) return ''
      short = value.substr(0,73)
      if (boo) return short
      return value
      }
    },
    filters: {
      //add filters here
    }
  });
  $('.ui.dropdown')
  .dropdown();
$('.dropdown').dropdown({
 onChange: function() {
    var t = $(".dropdown").dropdown("get value");
    return app.compare = t.split(","),
    Cookies.set('compare', t, { expires: 365 });
 }
});
$('.ui.inline.dropdown').dropdown({
 onChange: function() {
  $(".dimmable").dimmer("hide");
  var eval = $('.ui.inline.dropdown').dropdown('get value');
  if (eval.includes("monthly")) {
    return app.rank = monthly, 
    app.banner = "Lowest Monthly Price",
    app.rankby="monthly"
  } else if (eval.includes("smart")) {
    return app.rank = smart,
    app.banner = "Best Smart Home",
    app.rankby="smart"
  }else if (eval.includes("contract")) {
    return app.rank = contract,
    app.banner = "Best Contract Terms",
    app.rankby="contract"
  }else if (eval.includes("costs")) {
    return app.rank = cost,
    app.banner = "Lowest Entry Costs",
    app.rankby="entryCosts"
  }else if (eval.includes("editor")) {
    return app.rank = editor,
    app.banner =  "Editor's Choice",
    app.rankby="editor"
  }
  
  
 }
});
</script>


</body>

</html>
