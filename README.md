# Delete-Produto.PHP
Criação do código do deleteproduto.php funcional para completar o CRUD no sistema.

<?php
include('conn.php');
if($_SERVER['REQUEST_METHOD']=='POST'){
    $id = $_POST['id'];
    $sql = "UPDATE tb_produtos SET status_produto = 0 WHERE id_produto = $id";
    mysqli_query($link,$sql);
    mysqli_close($link);
    header('Location: listaprodutos.php');
    exit();
}

if(!isset($_GET['id'])){
    header('Location:listaprodutos.php');
    exit();
}

$id = $_GET['id'];
$sql = "SELECT nome_produto FROM tb_produtos WHERE id_produto = $id";
$result = mysqli_query($link,$sql);
$tbl = mysqli_fetch_array($result);
mysqli_close($link);

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
