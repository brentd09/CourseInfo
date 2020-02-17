# How to calculate subnets 
## Given scenario

## 130.4.0.0/16 address has been aquired for subnetting
## 5 subnets are required
## 2000 host IP addresses / subnet are required

## Step 1 

**How many bits do we need to trade from the hosts to accomodate the networks required**


**2<sup>1</sup>=2**<br>
**2<sup>2</sup>=4**<br>
**2<sup>3</sup>=8**<br>
**2<sup>4</sup>=16**<br>
**2<sup>5</sup>=32**<br>
**2<sup>6</sup>=64**<br>
**2<sup>7</sup>=128**<br>
**2<sup>8</sup>=256**<br>
**This shows us:**<br><br>
**to get 4 subnets we need to trade 2 host bits to networks**<br> 
**to get 8 subnets we need to trade 3 host bits to networks**<br><br> 
**In this case 4 subnets (trading 2 host bits to networks) therefore we need to trade 3 host bits, giving us least 8 networks. We could trade more host bits giving us more networks, however we would also need to make sure we have enough host bits left to accomodate the required hosts/subnet requirements.<br> 
