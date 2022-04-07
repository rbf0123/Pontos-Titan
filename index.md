<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta nome="viewport" content="width=device=width, initial-scale=1.0">
     <title>Controle de E-mails</title>

     <style>
         body{
             font-family: Arial, Helvetica, sans-serif;
         }
         table{
             border-collapse: collapse;
         }
         caption {
            font-size: 1.2em;
            font-weight: bolder;
            padding: 20px;
         }

         th, td{
             border: 1px solid black;
             padding: 10px;
         }
         tr:nth-child(even){
             background-color: rgb(228, 228, 228);
         }

         div#container{
             overflow-x: auto ;
         }
      
           
     </style>

</head> 




<body>
   <h1>Cálculo de Pontos </h1>
   <p>Para calcular a quantidade de pontos selecione na tabela os bairros desejado! </p> 

  

   
   <div id="container">
    <table>
        <caption>Tabela de Pontos</caption>
       <thead>
        <tr>
            <th>Bairro</th>
            <th>Ponto</th> 
            <th>Observação</th> 
        </tr>

        </thead>

        <tbody>

<!--Itens listado na tabela de bairros-->
          <tr>
            <td><center>Sto. Amaro</center></td>
            <td><center>3</center></td>
            <td><center><label> <input type="checkbox" name="ch[]" value="3" /></label></center></td>
          </tr>

          <tr>
            <td><center>Vila Nova Conceição</center></td>
            <td><center>2</center></td>
            <td><center><label> <input type="checkbox" name="ch[]" value="2" /></label></center></td>
          </tr>

          <tr>
            <td><center>Itaim Bibi</center></td>
            <td><center>3</center></td>
            <td><center><label> <input type="checkbox" name="ch[]" value="3" /></label></center></td>
          </tr>

          <tr>
            <td><center>Consolação</center></td>
            <td><center>5</center></td>
            <td><center><label> <input type="checkbox" name="ch[]" value="5" /></label></center></td>
          </tr>
     
          <!--Excluir o "R$" do value=!!R$ 0,00 da linha LABEL antes do script e 
                        "R$$" do  result.value = "!!R$ " + String(result).formatMoney(); -->
          <label><center>Total de Pontos <input type="text" name="result" id="result" value="0,00 " /></center></label>


<!--Script checa se a caixa está selecionada, se sim, soma os valores, senão, subtrai o valor-->
          <script>

            String.prototype.formatMoney = function() {
                var v = this;
            
                if(v.indexOf('.') === -1) {
                    v = v.replace(/([\d]+)/, "$1,00");
                }
            
                v = v.replace(/([\d]+)\.([\d]{1})$/, "$1,$20");
                v = v.replace(/([\d]+)\.([\d]{2})$/, "$1,$2");
                v = v.replace(/([\d]+)([\d]{3}),([\d]{2})$/, "$1.$2,$3");
            
                return v;
            };
            String.prototype.toFloat = function() {
                var v = this;
            
                if (!v) return 0;
                return parseFloat(v.replace(/[\D]+/g, '' ).replace(/([\d]+)(\d{2})$/, "$1.$2"));
            };
            (function(){
                "use strict";
            
                var $chs = document.querySelectorAll('input[name="ch[]"]'),
                    $result = document.getElementById('result'),
                    chsArray = Array.prototype.slice.call($chs);
            
                chsArray.forEach(function(element, index, array){
                    element.addEventListener("click", function(){
                        var v = this.value,
                            result = 0;
                        v = v.toFloat();
            
                        if (this.checked === true) {
                            result = $result.value.toFloat() + parseFloat(v);
                        } else {
                            result = $result.value.toFloat() - parseFloat(v);
                        }
                        
                    

                        $result.value = " " + String(result).formatMoney();
          
                    });
                });

                
                        
            }());

            </script>
        </tbody>
    </table>
</div>
   
   
</body>

</html>
