# Sistema de Arquivos Formato EXT3

## Definição
O Ext3  é um sistema de arquivos desenvolvido por Stephen C. Tweedie para o UNIX, que tira alguns recursos ao Ext2, dos quais o mais visível é o journaling ou diário. O sistema de arquivos ext3 ou prorrogado terceiro é um sistema de arquivos com diário que é comumente usada pelo kernel Linux. É o padrão do sistema de arquivos para muitos populares distribuições Linux. Stephen C. Tweedie primeiro revelou que ele estava trabalhando na extensão ext2 no Diário do Linux ext2fs Filesystem em um documento de 1998 e mais tarde em uma lista de discussão do destacamento kernel em fevereiro de 1999, e o sistema de arquivos foi fundida com a a linha principal do kernel do Linux em novembro de 2001. Sua principal vantagem sobre ext2 é o diário, que melhora a confiabilidade e elimina a necessidade de verificar o sistema de arquivos após um desligamento abrupto. Seu sucessor é o Ext4.
___

## Vantagens

A performance (velocidade) do Ext3 é menos atrativa do que os sistemas de arquivos competidores do Linux, como o Ext4, JFS, ReiserFS e XFS, mas o Ext3 tem uma vantagem significativa que o permite realizar upgrades no lugar do Ext2 sem precisar de fazer backup e restauração dos dados.

Benchmarks sugerem que o Ext3 também usa menos processamento que ReiserFS e XFS. Este é tambem considerado mais seguro que outros sistemas de arquivos Linux, devido a sua relativa simplicidade e ampla base de testes.

### Journaling 
A principal diferença entre o Ext2 e o Ext3 é a implementação do journaling, que consiste em um registro (log ou journal) de transações cuja finalidade é recuperar o sistema em caso de desligamento não programado.

Há três níveis de journaling disponíveis na implementação do Ext3:


- Journal: os metadados e os dados (conteúdo) dos arquivos são escritos no journal antes de serem de fato escritos no sistema de arquivos principal. Isso aumenta a confiabilidade do sistema, porém com uma perda de desempenho, devido à necessidade dos dados serem escritos duas vezes no disco.

- Writeback: os metadados são escritos no journal mas não o conteúdo dos arquivos. Essa opção permite um melhor desempenho em relação ao modo journal, porém introduz o risco de escrita fora de ordem onde, por exemplo, arquivos que são apensados durante um crash podem ter adicionados a eles trechos de lixo na próxima montagem.

- Ordered: é como o writeback, mas força que a escrita do conteúdo dos arquivos seja feita após a marcação de seus metadados como escritos no journal. Esse é considerado um meio-termo aceitável entre confiabilidade e performance, sendo, portanto, o nível padrão.

Embora o seu desempenho (velocidade) seja menos atrativo que o de outros sistemas de arquivos (como ReiserFS e XFS), ele tem a importante vantagem de permitir que seja feita a atualização direta a partir de um sistema com ext2, sem a necessidade de realizar um backup e restaurar posteriormente os dados, bem como o menor consumo de processamento.

___

## Desvantagens
### Funcionalidade
A estrutura da partição ext3 é semelhante à da ext2, pelo que a migração de um formato para o outro é simples. A adição do journaling é feita em um arquivo chamado *journal* que fica oculto pelo código ext3 na partição (desta forma ele não poderá ser apagado, o que comprometeria o funcionamento do sistema). A estrutura idêntica da partição ext3 com a ext2 torna mais fácil a manutenção do sistema, já que todas as ferramentas para recuperação ext2 funcionarão sem problemas, sendo mesmo possível montar uma partição ext3 como se fosse ext2.

Como o ext3 visa uma grande compatibilidade com o ext2, muitas das estruturas on-disk são similares àquelas da ext2. Por causa disso, o ext3 não possui muitas das funções mais recentes como alocação dinâmica de inodes e tamanhos de blocos variáveis (fragmentos ou caudas).

Os sistemas de arquivos ext3 não podem ser checados enquanto são montados para escrita. Um dump do sistema de arquivos feito enquanto ele está sendo montado para leitura e escrita pode resultar em dados corrompidos dentro do arquivo de dump.

### Desfragmentação
Não há uma ferramenta online de desfragmentação funcional em nível de sistema de arquivos. Um desfragmentador offline da ext2, e2defrag, existe mas requer que um sistema ext3 seja revertido previamente ao ext2. Mas, dependendo das funcionalidades ativadas no sistema de arquivos, o e2defrag pode destruir dados; ele não sabe lidar com muitas das novas funcionalidades do ext3.

### Compressão
Suporte a compressão transparente de dados (disponível como um patch extra-oficial para ext2) não está disponível no ext3.

O ext3 tem um tamanho máximo para arquivos e para o sistema de arquivos inteiro. Esses limites dependem do tamanho de bloco do sistema de arquivos; a tabela abaixo resume esses limites:

| Tamanho do bloco |	Tamanho máx. arquivo |	Tamanho máx. fs |
|:----------------:|:---------------------:|:----------------:|
| 1 KiB | 16 GiB | 4 TiB |
| 2 KiB |	256 GiB |	8 TiB |
| 4 KiB |	2 TiB | 16 TiB |
| 8 KiB |	2 TiB |	32 TiB |

O tamanho de bloco de 8 KiB está apenas disponível para arquiteturas que permitem paginação de 8 KiB.

___

## Referências
> TS'O, Theodore Y.; TWEEDIE, Stephen. Planned extensions to the Linux Ext2/Ext3 filesystem. Proceedings of Usenix 2002 Annual Technical Conference. 2002. pp. 235–244. Disponível em <http://e2fsprogs.sourceforge.net/extensions-ext23/extensions-ext23.pdf>. Acesso em 16 de novembro 2017.
