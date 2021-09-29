$login = 'diegonunesmkt2@gmail.com';
$senha = '230106ka';

$str_conexao = '{imap.gmail.com:993/imap/ssl}';
if (!extension_loaded('imap')) {
    die('Modulo PHP/IMAP nao foi carregado');
}
$mailbox = imap_open($str_conexao, $login, $senha);
if (!$mailbox) {
    die('Erro ao conectar: '.imap_last_error());
}
$check = imap_check($mailbox);

echo $check->Date;

echo $check->Driver;

echo $check->Mailbox;

echo $check->Nmsgs;

echo $check->Recent;
$marcadores = imap_getmailboxes($mailbox, $str_conexao, '*');

if (is_array($marcadores)) {
    foreach ($marcadores as $marcador) {
        $nome = str_replace($str_conexao, '', $marcador->name);
        $pos = strpos($nome, $marcador->delimiter);
        if ($pos !== false) {
            $nome = substr($nome, $pos + 1);
        }
        echo $nome."\n";
    }
} else {
    echo imap_last_error();
}
$overview = imap_fetch_overview($mailbox, 1);

$email = current($overview);

echo $email->subject;

echo $email->from;

echo $email->to;

echo $email->date;

echo $email->message_id;

echo $email->references;

echo $email->in_reply_to;

echo $email->size;

echo $email->uid;

echo $email->msgno;

echo $email->recent;

echo $email->flagged;

echo $email->answered;

echo $email->deleted;

echo $email->seen;

echo $email->draft;
