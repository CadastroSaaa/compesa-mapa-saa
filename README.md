# Cadastro Técnico SAA — Pernambuco

Mapa web interativo com as camadas técnicas de Abastecimento de Água (SAA) da Compesa,
gerado a partir do cadastro QGIS original (itens 25, 26 e 29).

## Conteúdo

- `index.html` — página do mapa (MapLibre GL JS)
- `compesa_saa_rest.pmtiles` — 18 camadas técnicas (rede, adutoras, reservatórios, válvulas,
  medidores, etc.), ~72 MB
- `micromedidor_cluster.pmtiles` — camada de Micromedidor (285 mil pontos), com agrupamento
  visual por zoom (clustering), ~17,5 MB

Total: ~86 MB — dentro do limite de 100 MB por arquivo do GitHub.

## Como publicar no GitHub Pages

1. Crie um repositório novo no GitHub (pode ser privado se preferir acesso restrito à equipe,
   mas Pages em repositório privado exige plano GitHub Pro/Team/Enterprise — em repositório
   público o Pages é gratuito e o link funciona para qualquer pessoa com o link).
2. Faça upload dos 3 arquivos desta pasta para a raiz do repositório (pode arrastar e soltar
   na interface web do GitHub, em "Add file" → "Upload files").
3. Vá em **Settings → Pages**.
4. Em "Source", selecione **Deploy from a branch**, branch **main**, pasta **/ (root)**.
5. Salve e aguarde 1–2 minutos. O GitHub vai gerar um link do tipo:
   `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`
6. Esse é o link que pode ser compartilhado com a equipe.

## Limitações conhecidas

- A busca por matrícula/código só encontra resultados nas camadas/tiles já carregados na
  área visível do mapa (é uma limitação de mapas baseados em tiles estáticos, sem banco de
  dados rodando por trás). Navegue até a região aproximada antes de buscar.
- Apenas 1,1% dos micromedidores e a maioria das válvulas/redes não têm CODID preenchido na
  fonte original da Compesa — não é uma falha desta ferramenta, é uma lacuna do cadastro.
- As camadas de Esgotamento Sanitário (SES) não estão incluídas nesta versão, para manter o
  arquivo abaixo do limite de tamanho do GitHub. Podem ser adicionadas depois como um
  segundo mapa/link, seguindo o mesmo processo.

## Atualizando os dados no futuro

Caso o cadastro técnico seja atualizado no QGIS, o processo para regenerar este mapa é:
1. Exportar os shapefiles atualizados do QGIS.
2. Limpar campos de auditoria desnecessários (created_us, last_edite, campos "d_*").
3. Converter para GeoJSON (EPSG:4326).
4. Gerar tiles vetoriais com tippecanoe.
5. Converter para pmtiles.
6. Substituir os arquivos .pmtiles neste repositório.

Se quiser ajuda para repetir esse processo, é só voltar nesta conversa ou abrir uma nova com
os arquivos atualizados.
