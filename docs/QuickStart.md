```
       ctl-opt option(*nodebugio:*srcstmt) bnddir('RPGWEB')
              dftactgrp(*no);

      /copy RPGWEB/qrpglesrc,RPGWEB_H

       dcl-ds request likeds(RPGWEBRQST);
       dcl-ds response likeds(RPGWEBRSP);
       dcl-ds app likeds(RPGWEBAPP);

       clear app;

       RPGWEB_get(app : '/hello' : %paddr(test_proc));

       RPGWEB_start(app: 3017);

       *inlr = *on;
       return;


       dcl-proc test_proc;
         dcl-pi *n likeds(RPGWEBRSP);
           request likeds(RPGWEBRQST) const;
         end-pi;

         response.body = 'hello';
         response.status = HTTP_OK;
         RPGWEB_setHeader(response : 'Content-Type' : 'application/text');

         return response;
       end-proc;
```