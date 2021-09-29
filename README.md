$login = 'diegonunesmkt2@gmail.com';
$senha = '';

$str_conexao = '{imap.gmail.com:993/imap/ssl}';
if (!extension_loaded('imap')) {
    die('Modulo PHP/IMAP nao foi carregado');
}
$mailbox = imap_open($str_conexao, $login, $senha);
if (!$mailbox) {
    die('Erro ao conectar: '.imap_last_error());
}
$check = imap_check($mailbox);

$check->Date;

$check->Driver;

$check->Mailbox;

$check->Nmsgs;

$check->Recent;
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

$email->subject;

$email->from;

$email->to;

$email->date;

$email->message_id;

$email->references;

$email->in_reply_to;

$email->size;

$email->uid;

$email->msgno;

$email->recent;

$email->flagged;

$email->answered;

$email->deleted;

$email->seen;

$email->draft;
