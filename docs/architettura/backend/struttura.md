# Struttura

```
src
 ┣ @types
 ┃ ┣ express
 ┃ ┃ ┗ index.d.ts
 ┃ ┣ ImportMensile.ts
 ┃ ┣ ImportRinnovo.ts
 ┃ ┣ OrderConfiguration.ts
 ┃ ┗ SerialActivation.ts
 ┣ config
 ┃ ┣ cors.ts
 ┃ ┣ csp.ts
 ┃ ┣ fileUpload.ts
 ┃ ┣ morgan.ts
 ┃ ┣ sequelize.ts
 ┃ ┣ swagger.ts
 ┃ ┗ winston.ts
 ┣ controllers
 ┃ ┣ ArticleChangeCtrl.ts
 ┃ ┣ ArticleParentCtrl.ts
 ┃ ┣ ArticoloClienteOrdineCtrl.ts
 ┃ ┣ ArticoloCtrl.ts
 ┃ ┣ ArticoloMensileCtrl.ts
 ┃ ┣ ArticoloOrdineCtrl.ts
 ┃ ┣ ArticoloPropostaCtrl.ts
 ┃ ┣ ArticoloRinnovoCtrl.ts
 ┃ ┣ ArticoloRinnovoStoricoCtrl.ts
 ┃ ┣ AttivazioneArticoloOrdineCtrl.ts
 ┃ ┣ CambioPianoCtrl.ts
 ┃ ┣ ClienteCtrl.ts
 ┃ ┣ ConfigurazioneMensileLocaleCtrl.ts
 ┃ ┣ ConfigurazioneRinnovoLocaleCtrl.ts
 ┃ ┣ ContattoCtrl.ts
 ┃ ┣ CostruttoreCtrl.ts
 ┃ ┣ DisdettaCtrl.ts
 ┃ ┣ GruppoCassaincloudCtrl.ts
 ┃ ┣ GruppoCtrl.ts
 ┃ ┣ LocaleCtrl.ts
 ┃ ┣ MacroTipoArticoloCtrl.ts
 ┃ ┣ MailCtrl.ts
 ┃ ┣ MatricolaArticoloOrdineCtrl.ts
 ┃ ┣ MensileCtrl.ts
 ┃ ┣ MotivazioneCtrl.ts
 ┃ ┣ NumbersCtrl.ts
 ┃ ┣ OrdineCtrl.ts
 ┃ ┣ PDFCtrl.ts
 ┃ ┣ PagamentoMensileCtrl.ts
 ┃ ┣ PrezzoCtrl.ts
 ┃ ┣ ProfiloContattoCtrl.ts
 ┃ ┣ ProfiloLocaleCtrl.ts
 ┃ ┣ PropostaCtrl.ts
 ┃ ┣ RepartoCtrl.ts
 ┃ ┣ RinnovoCtrl.ts
 ┃ ┣ StatoCtrl.ts
 ┃ ┣ TPaymentEsattoCtrl.ts
 ┃ ┣ TTraceCtrl.ts
 ┃ ┣ TipoArticoloCtrl.ts
 ┃ ┣ TipoFatturazioneCtrl.ts
 ┃ ┣ TipoGruppoCtrl.ts
 ┃ ┣ TipoOrdineCtrl.ts
 ┃ ┗ UtenteCtrl.ts
 ┣ crons
 ┃ ┣ import_mensili_cron.ts
 ┃ ┗ import_rinnovi_cron.ts
 ┣ images
 ┃ ┣ .DS_Store
 ┃ ┣ logo_rca.png
 ┃ ┣ placeholder.png
 ┃ ┗ placeholder_black.png
 ┣ logs
 ┃ ┣ debug
 ┃ ┃ ┗ YYYY-MM-DD.log
 ┃ ┣ error
 ┃ ┃ ┗ YYYY-MM-DD.log
 ┃ ┣ http
 ┃ ┃ ┗ YYYY-MM-DD.log
 ┃ ┣ info
 ┃ ┃ ┗ YYYY-MM-DD.log
 ┃ ┣ mail
 ┃ ┃ ┗ YYYY-MM-DD.log
 ┃ ┣ sequelize
 ┃ ┃ ┗ YYYY-MM-DD.log
 ┃ ┣ socket
 ┃ ┃ ┣ percentuale.log
 ┃ ┃ ┗ report.log
 ┃ ┗ .DS_Store
 ┣ middlewares
 ┃ ┣ editStatusCheck.middleware.ts
 ┃ ┣ extractOptions.middleware.ts
 ┃ ┣ jwt.auth.ts
 ┃ ┣ privilegiOrdineUtente.middleware.ts
 ┃ ┗ sequelizeMapping.middleware.ts
 ┣ models
 ┃ ┣ article_change.ts
 ┃ ┣ article_parent.ts
 ┃ ┣ articolo.ts
 ┃ ┣ articolo_cliente_ordine.ts
 ┃ ┣ articolo_mensile.ts
 ┃ ┣ articolo_ordine.ts
 ┃ ┣ articolo_proposta.ts
 ┃ ┣ articolo_rinnovo.ts
 ┃ ┣ articolo_rinnovo_storico.ts
 ┃ ┣ attivazione_articolo_ordine.ts
 ┃ ┣ cambio_piano.ts
 ┃ ┣ cliente.ts
 ┃ ┣ configurazione_mensile_locale.ts
 ┃ ┣ configurazione_rinnovo_locale.ts
 ┃ ┣ contatto.ts
 ┃ ┣ costruttore.ts
 ┃ ┣ disdetta.ts
 ┃ ┣ gruppo.ts
 ┃ ┣ gruppo_cassaincloud.ts
 ┃ ┣ init-models.ts
 ┃ ┣ locale.ts
 ┃ ┣ macro_tipo_articolo.ts
 ┃ ┣ matricola_articolo_ordine.ts
 ┃ ┣ mensile.ts
 ┃ ┣ motivazione.ts
 ┃ ┣ numbers.ts
 ┃ ┣ ordine.ts
 ┃ ┣ pagamento_mensile.ts
 ┃ ┣ prezzo.ts
 ┃ ┣ profilo_contatto.ts
 ┃ ┣ profilo_locale.ts
 ┃ ┣ proposta.ts
 ┃ ┣ reparto.ts
 ┃ ┣ rinnovo.ts
 ┃ ┣ stato.ts
 ┃ ┣ t_payment_esatto.ts
 ┃ ┣ t_trace.ts
 ┃ ┣ tipo_articolo.ts
 ┃ ┣ tipo_fatturazione.ts
 ┃ ┣ tipo_gruppo.ts
 ┃ ┣ tipo_ordine.ts
 ┃ ┗ utente.ts
 ┣ pre-start
 ┃ ┣ env
 ┃ ┃ ┣ development.env
 ┃ ┃ ┣ production.env
 ┃ ┃ ┗ test.env
 ┃ ┗ index.ts
 ┣ public
 ┃ ┣ docs
 ┃ ┣ frontend
 ┃ ┃ ┣ css
 ┃ ┃ ┃ ┣ app.5b757f3b.css
 ┃ ┃ ┃ ┗ chunk-vendors.aaf76455.css
 ┃ ┃ ┣ js
 ┃ ┃ ┃ ┣ app.477e768d.js
 ┃ ┃ ┃ ┣ app.477e768d.js.map
 ┃ ┃ ┃ ┣ chunk-vendors.aa68b2bd.js
 ┃ ┃ ┃ ┗ chunk-vendors.aa68b2bd.js.map
 ┃ ┃ ┣ vendors
 ┃ ┃ ┃ ┗ bootstrap.bundle.min.js
 ┃ ┃ ┣ custom.css
 ┃ ┃ ┣ favicon.ico
 ┃ ┃ ┣ index.html
 ┃ ┃ ┣ logo.png
 ┃ ┃ ┣ t-order.svg
 ┃ ┃ ┗ torder_logo.png
 ┃ ┣ scripts
 ┃ ┃ ┣ init_guest_home.js
 ┃ ┃ ┗ redoc.standalone.js
 ┃ ┗ openapi.json
 ┣ repositories
 ┃ ┣ ArticleChangeRepo.ts
 ┃ ┣ ArticleParentRepo.ts
 ┃ ┣ ArticoloClienteOrdineRepo.ts
 ┃ ┣ ArticoloMensileRepo.ts
 ┃ ┣ ArticoloOrdineRepo.ts
 ┃ ┣ ArticoloPropostaRepo.ts
 ┃ ┣ ArticoloRepo.ts
 ┃ ┣ ArticoloRinnovoRepo.ts
 ┃ ┣ ArticoloRinnovoStoricoRepo.ts
 ┃ ┣ AttivazioneArticoloOrdineRepo.ts
 ┃ ┣ CambioPianoRepo.ts
 ┃ ┣ ClienteRepo.ts
 ┃ ┣ ConfigurazioneMensileLocaleRepo.ts
 ┃ ┣ ConfigurazioneRinnovoLocaleRepo.ts
 ┃ ┣ ContattoRepo.ts
 ┃ ┣ CostruttoreRepo.ts
 ┃ ┣ DisdettaRepo.ts
 ┃ ┣ GruppoCassaincloudRepo.ts
 ┃ ┣ GruppoRepo.ts
 ┃ ┣ LocaleRepo.ts
 ┃ ┣ MacroTipoArticoloRepo.ts
 ┃ ┣ MatricolaArticoloOrdineRepo.ts
 ┃ ┣ MensileRepo.ts
 ┃ ┣ MotivazioneRepo.ts
 ┃ ┣ NumbersRepo.ts
 ┃ ┣ OrdineRepo.ts
 ┃ ┣ PagamentoMensileRepo.ts
 ┃ ┣ PrezzoRepo.ts
 ┃ ┣ ProfiloContattoRepo.ts
 ┃ ┣ ProfiloLocaleRepo.ts
 ┃ ┣ PropostaRepo.ts
 ┃ ┣ RepartoRepo.ts
 ┃ ┣ RinnovoRepo.ts
 ┃ ┣ StatoRepo.ts
 ┃ ┣ TPaymentEsattoRepo.ts
 ┃ ┣ TipoArticoloRepo.ts
 ┃ ┣ TipoFatturazioneRepo.ts
 ┃ ┣ TipoGruppoRepo.ts
 ┃ ┣ TipoOrdineRepo.ts
 ┃ ┣ TraceRepo.ts
 ┃ ┗ UtenteRepo.ts
 ┣ routes
 ┃ ┣ AccessToken.route.ts
 ┃ ┣ ArticleChange.route.ts
 ┃ ┣ ArticleParent.route.ts
 ┃ ┣ Articolo.route.ts
 ┃ ┣ ArticoloClienteOrdine.route.ts
 ┃ ┣ ArticoloMensile.route.ts
 ┃ ┣ ArticoloOrdine.route.ts
 ┃ ┣ ArticoloProposta.route.ts
 ┃ ┣ ArticoloRinnovo.route.ts
 ┃ ┣ ArticoloRinnovoStorico.route.ts
 ┃ ┣ AttivazioneArticoloOrdine.route.ts
 ┃ ┣ CambioPiano.route.ts
 ┃ ┣ Cliente.route.ts
 ┃ ┣ ConfigurazioneMensileLocale.route.ts
 ┃ ┣ ConfigurazioneRinnovoLocale.route.ts
 ┃ ┣ Contatto.route.ts
 ┃ ┣ Costruttore.route.ts
 ┃ ┣ Disdetta.route.ts
 ┃ ┣ File.route.ts
 ┃ ┣ Gruppo.route.ts
 ┃ ┣ GruppoCassaincloud.route.ts
 ┃ ┣ Guest.route.ts
 ┃ ┣ Locale.route.ts
 ┃ ┣ Logs.route.ts
 ┃ ┣ MacroTipoArticolo.route.ts
 ┃ ┣ Mail.route.ts
 ┃ ┣ MatricolaArticoloOrdine.route.ts
 ┃ ┣ Mensile.route.ts
 ┃ ┣ Motivazione.route.ts
 ┃ ┣ Numbers.route.ts
 ┃ ┣ Ordine.route.ts
 ┃ ┣ PDF.route.ts
 ┃ ┣ PagamentoMensile.route.ts
 ┃ ┣ Prezzo.route.ts
 ┃ ┣ ProfiloContatto.route.ts
 ┃ ┣ ProfiloLocale.route.ts
 ┃ ┣ Proposta.route.ts
 ┃ ┣ Reparto.route.ts
 ┃ ┣ Rinnovo.route.ts
 ┃ ┣ Stato.route.ts
 ┃ ┣ TPaymentEsatto.route.ts
 ┃ ┣ Test.route.ts
 ┃ ┣ TipoArticolo.route.ts
 ┃ ┣ TipoFatturazione.route.ts
 ┃ ┣ TipoGruppo.route.ts
 ┃ ┣ TipoOrdine.route.ts
 ┃ ┣ Trace.route.ts
 ┃ ┣ Utente.route.ts
 ┃ ┗ index.ts
 ┣ services
 ┃ ┣ Auth0Mangement.service.ts
 ┃ ┣ Encrypt.service.ts
 ┃ ┣ FileManager.service.ts
 ┃ ┣ Mailing.service.ts
 ┃ ┣ PDFGenerator.service.ts
 ┃ ┣ QrCodeGenerator.service.ts
 ┃ ┗ Telegram.service.ts
 ┣ shared
 ┃ ┣ api_error_handler.ts
 ┃ ┣ constants.ts
 ┃ ┣ fillTemplate.ts
 ┃ ┣ functions.ts
 ┃ ┣ hashCode.ts
 ┃ ┣ sqlize_models_mapping.ts
 ┃ ┗ sqlize_op_mapping.ts
 ┣ sockets
 ┃ ┣ main.socket.ts
 ┃ ┗ watch.approach.socket.ts
 ┣ templates
 ┃ ┣ order.template.html
 ┃ ┣ ordine_rinnovo.template.html
 ┃ ┗ preventivo.template.html
 ┣ uploads
 ┃ ┣ ordini
 ┃ ┃ ┣ 12418
 ┃ ┃ ┣ 12863
 ┃ ┃ ┣ 12934
 ┃ ┃ ┣ 12938
 ┃ ┃ ┣ 12939
 ┃ ┃ ┃ ┗ docs2.html
 ┃ ┃ ┣ 12944
 ┃ ┃ ┣ 12952
 ┃ ┃ ┗ .DS_Store
 ┃ ┣ temp
 ┃ ┃ ┣ 1650466151379
 ┃ ┃ ┃ ┗ R-24187.pdf
 ┃ ┃ ┣ 1650791825997
 ┃ ┃ ┃ ┗ O-12944.pdf
 ┃ ┃ ┣ 1650811644623
 ┃ ┃ ┃ ┗ O-12944.pdf
 ┃ ┃ ┣ 1650811712608
 ┃ ┃ ┃ ┗ O-12941.pdf
 ┃ ┃ ┣ 1650833591425
 ┃ ┃ ┃ ┗ O-12944.pdf
 ┃ ┃ ┣ 1650842440375
 ┃ ┃ ┃ ┗ O-12944.pdf
 ┃ ┃ ┣ 1650842547460
 ┃ ┃ ┃ ┗ O-12944.pdf
 ┃ ┃ ┣ 1650842763732
 ┃ ┃ ┃ ┗ O-12944.pdf
 ┃ ┃ ┣ 1650842825178
 ┃ ┃ ┃ ┗ R-24245.pdf
 ┃ ┃ ┣ 1650842853416
 ┃ ┃ ┃ ┗ O-12944.pdf
 ┃ ┃ ┣ 1650878554880
 ┃ ┃ ┃ ┗ R-24245.pdf
 ┃ ┃ ┣ 1650885652306
 ┃ ┃ ┃ ┗ O-12944.pdf
 ┃ ┃ ┣ 1650885880065
 ┃ ┃ ┃ ┗ O-12944.pdf
 ┃ ┃ ┣ 1650885947963
 ┃ ┃ ┃ ┗ O-12944.pdf
 ┃ ┃ ┣ 1651578136585
 ┃ ┃ ┃ ┗ R-24194.pdf
 ┃ ┃ ┣ 1651653452992
 ┃ ┃ ┃ ┗ O-12952.pdf
 ┃ ┃ ┣ 1651661753954
 ┃ ┃ ┃ ┗ R-24194.pdf
 ┃ ┃ ┣ 1651670766678
 ┃ ┃ ┃ ┗ O-12951.pdf
 ┃ ┃ ┣ 1651670773724
 ┃ ┃ ┃ ┗ R-24194.pdf
 ┃ ┃ ┣ 1652124450182
 ┃ ┃ ┃ ┗ R-26045.pdf
 ┃ ┃ ┣ 1652195941204
 ┃ ┃ ┃ ┗ R-25298.pdf
 ┃ ┃ ┣ 1652197890419
 ┃ ┃ ┃ ┗ R-25310.pdf
 ┃ ┃ ┣ 1652969139256
 ┃ ┃ ┃ ┗ O-13016.pdf
 ┃ ┃ ┣ 1654504012914
 ┃ ┃ ┃ ┗ R-39321.pdf
 ┃ ┃ ┗ 1654505224913
 ┃ ┃ ┃ ┗ R-39321.pdf
 ┃ ┗ .DS_Store
 ┣ validators
 ┃ ┣ ArticleChangeValidator.ts
 ┃ ┣ ArticleParentValidator.ts
 ┃ ┣ ArticoloClienteOrdineValidator.ts
 ┃ ┣ ArticoloMensileValidator.ts
 ┃ ┣ ArticoloOrdineValidator.ts
 ┃ ┣ ArticoloPropostaValidator.ts
 ┃ ┣ ArticoloRinnovoStoricoValidator.ts
 ┃ ┣ ArticoloRinnovoValidator.ts
 ┃ ┣ ArticoloValidator.ts
 ┃ ┣ AttivazioneArticoloOrdineValidator.ts
 ┃ ┣ CambioPianoValidator.ts
 ┃ ┣ ClienteValidator.ts
 ┃ ┣ ConfigurazioneMensileLocaleValidator.ts
 ┃ ┣ ConfigurazioneRinnovoLocaleValidator.ts
 ┃ ┣ ContattoValidator.ts
 ┃ ┣ CostruttoreValidator.ts
 ┃ ┣ DisdettaValidator.ts
 ┃ ┣ GruppoCassaincloudValidator.ts
 ┃ ┣ GruppoValidator.ts
 ┃ ┣ LocaleValidator.ts
 ┃ ┣ MacroTipoArticoloValidator.ts
 ┃ ┣ MailValidator.ts
 ┃ ┣ MatricolaArticoloOrdineValidator.ts
 ┃ ┣ MensileValidator.ts
 ┃ ┣ MotivazioneValidator.ts
 ┃ ┣ NumbersValidator.ts
 ┃ ┣ OrdineValidator.ts
 ┃ ┣ PagamentoMensileValidator.ts
 ┃ ┣ PrezzoValidator.ts
 ┃ ┣ ProfiloContattoValidator.ts
 ┃ ┣ ProfiloLocaleValidator.ts
 ┃ ┣ PropostaValidator.ts
 ┃ ┣ RepartoValidator.ts
 ┃ ┣ RinnovoValidator.ts
 ┃ ┣ StatoValidator.ts
 ┃ ┣ TPaymentEsattoValidator.ts
 ┃ ┣ TTraceValidator.ts
 ┃ ┣ TipoArticoloValidator.ts
 ┃ ┣ TipoFatturazioneValidator.ts
 ┃ ┣ TipoGruppoValidator.ts
 ┃ ┣ TipoOrdineValidator.ts
 ┃ ┗ UtenteValidator.ts
 ┣ views
 ┃ ┣ guest.ejs
 ┃ ┗ redoc_docs.ejs
 ┣ .DS_Store
 ┣ Server.ts
 ┣ cluster.ts
 ┗ index.ts
```
