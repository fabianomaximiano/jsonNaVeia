# jsonNaVeia
<?php

    header( 'Content-type: application/json; charset="UTF-8"');

    $key = '669e2b9d25620aec5d5d289b47ded36b';
    $host = 'capitala-rest.vistahost.com.br'; // sandbox-rest.vistahost.com.br
    
    $dados = array(
                'fields' => array( 'Codigo', 'Cidade', 'Bairro', 'ValorVenda' ),
                'filter' => array( 'Finalidade' => 'Aluguel' ) // Aluguel, Venda
            );
    
    $url =  'http://'.$host.'/imoveis/listar?key=' . $key . '&pesquisa=' . json_encode( $dados );

    
    $ch = curl_init();
    
    $options = array(
                CURLOPT_RETURNTRANSFER => true,
                CURLOPT_HTTPHEADER => array( 'Accept: application/json' ),
                CURLOPT_URL => $url
            );
    
    curl_setopt_array( $ch, $options );
    
    $retorno = curl_exec( $ch );
    
    curl_close( $ch );
    
    $json = json_decode( $retorno, true );
    //print_r( $json );


    foreach($json as $j){
        echo "<br/>Cidade: " . $j['Cidade'];
        echo "<br/>Bairro: " . $j['Bairro'];
        echo "<br/>Valor: " . $j['ValorVenda'];
    }
    
?>
    
