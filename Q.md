First off Q has many implimentations ( AngularJS, Q for nodejs, etc )

Lets say you have your add function

    function add(v1, v2){
        var result = new Promise(function(resolve, reject){
            setTimeout(function(){
                resolve(v1 + v2);
            }, 0);
        });
        return result;
    }

and you want to add a bunch of numbers, but then add those!?
    1+1 and 2+2 and 3+3
    then the results added 2 + 4 + 6

But HOW?! ( Not like this )

    add(1, 1).then(function(result){
       return add(2,2).then(function(r2){
        return add(r2, result);
      });
    }).then(function(result2){
      return add(3,3).then(function(r3){
        return add(r3, result2);
      });
    }).then(function(){
      console.log('result:', result2);
    });

That's far too messy ( and not efficient, those aren't all truly dependent on each other in series )

    var Q = require('q');
    var promises = [add(1,1), add(2,2), add(3,3)];

    Q.spread(promises, function(r1, r2, r3){

        return add(r1, r2).then(function(r4){
            return add(r3, r4);
        });

    }).then(function(finalResult){
        console.log('finalResult:', finalResult);
    });
