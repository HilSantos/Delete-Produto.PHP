# Delete-Produto.PHP
Criação do código do deleteproduto.php funcional para completar o CRUD no sistema.

<?php
// Inclui arquivos de segurança, cabeçalho da página e conexão com o banco de dados //
include('segurancadez.php');
include('cabecalho.php');
include('conn.php');

// Verifica se o formulário foi enviado via POST (confirmação da exclusão) //
if($_SERVER['REQUEST_METHOD']=='POST'){
    $id = $_POST['id']; // Obtém o ID do produto a ser excluído //

    // Atualiza o status do produto para 0 (inativo ou excluído logicamente) //
    $sql = "UPDATE tb_produtos SET status_produto = 0 WHERE id_produto = $id";
    mysqli_query($link, $sql); // Executa a query //

    mysqli_close($link); // Fecha a conexão com o banco de dados //
    // Exibe uma mensagem de sucesso e redireciona para a lista de produtos //

    // Redireciona para a lista de produtos após a exclusão //
    header('Location: listaprodutos.php');
    exit();
}

// Verifica se o ID do produto foi passado via GET (acesso direto à página) //
if(!isset($_GET['id'])){
    // Se não houver ID, redireciona para a lista de produtos //
    header('Location:listaprodutos.php');
    exit();
}

// Obtém o ID do produto a partir da URL (GET request) //
include('conn.php'); // Inclui a conexão com o banco de dados //
if(!is_numeric($_GET['id'])){
    // Se o ID não for numérico, redireciona para a lista de produtos //
    header('Location:listaprodutos.php');
    exit();
}
// Se o ID for numérico, armazena na variável $id //
if(!isset($_GET['id']) || empty($_GET['id'])){
    // Se o ID não estiver definido ou estiver vazio, redireciona para a lista de produtos //
    header('Location:listaprodutos.php');
    exit();
}
if(!is_numeric($_GET['id'])){
    // Se o ID não for numérico, redireciona para a lista de produtos //
    header('Location:listaprodutos.php');
    exit();
}
// Se o ID for válido, armazena na variável $id //
$link = mysqli_connect('localhost', 'root', '', 'db_produtos'); // Conecta ao banco de dados //
$id = $_GET['id'];

// Busca o nome do produto no banco de dados para exibir na confirmação //
$sql = "SELECT nome_produto FROM tb_produtos WHERE id_produto = $id";
$result = mysqli_query($link, $sql);
$tbl = mysqli_fetch_array($result); // Armazena o resultado da consulta //

mysqli_close($link); // Fecha a conexão com o banco //
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Excluir produto</title>
    <link rel= "stylesheet" href="cadastra.css">
</head>
<body>
    <br>
    <h1>Excluir Produto</h1>
    <br>
    <form action="deleteproduto.php" method="post">
        <p>Deseja excluir o produto em questão? <b><?=$tbl[0]?></b>.</p>
        <p>O produto será excluido permanentemente.</p>
        <br><br>
        <input type="submit" value="Excluir">
        <a href="listaprodutos.php">
            <input type="button" value="voltar">
            <input type="hidden" name="id" value="<?=$id?>">
        </a>
    </form>
    
</body>
</html>
