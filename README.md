# Exclui-Produto.PHP
Criação do código do excluiproduto.php funcional para completar o CRUD no sistema.

<?php
include('conn.php');

// Verifica se foi passado o ID do produto
if (isset($_GET['id'])) {
    $id = intval($_GET['id']);

    // Opcional: excluir a imagem física (se desejar) — apenas se você salva as imagens em uma pasta
    /*
    $consultaImagem = mysqli_query($link, "SELECT imagem_produto FROM tb_produtos WHERE id_produto = $id");
    $linha = mysqli_fetch_assoc($consultaImagem);
    if ($linha && file_exists('imagens/' . $linha['imagem_produto'])) {
        unlink('imagens/' . $linha['imagem_produto']); // deleta o arquivo da pasta
    }
    */

    // Executa o comando de exclusão
    $sql = "DELETE FROM tb_produtos WHERE id_produto = $id";
    mysqli_query($link, $sql);

    mysqli_close($link);
    header("Location: listaprodutos.php");
    exit();
} else {
    echo "ID do produto não informado.";
}
