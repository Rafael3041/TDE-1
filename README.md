# TDE-1
<?php

// Lê o número de enfeites
$N = intval(fgets(STDIN));

// Lê a matriz de confiança
$matrix = [];
for ($i = 0; $i < $N; $i++) {
    $matrix[] = explode(' ', trim(fgets(STDIN)));
}

// Inicializa a melhor ordem
$bestOrder = range(1, $N);
$maxConfidence = 0;

// Testa todas as ordens possíveis
function fatorial($num) {
    $res = 1;
    for ($i = 2; $i <= $num; $i++) {
        $res *= $i;
    }
    return $res;
}

function permutacoes($array) {
    if (count($array) <= 1) {
        return [$array];
    }
    $result = [];
    foreach ($array as $key => $item) {
        $restantes = $array;
        unset($restantes[$key]);
        foreach (permutacoes(array_values($restantes)) as $perm) {
            $result[] = array_merge([$item], $perm);
        }
    }
    return $result;
}

$perms = permutacoes($bestOrder);

foreach ($perms as $perm) {
    $confidence = 1;
    for ($i = 0; $i < $N; $i++) {
        $confidence *= $matrix[$i][$perm[$i] - 1];
    }
    if ($confidence > $maxConfidence) {
        $maxConfidence = $confidence;
        $bestOrder = $perm;
    }
}

// Imprime a melhor ordem
echo implode(' ', $bestOrder) . "\n";

?>
