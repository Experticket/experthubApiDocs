
Ejemplo de petición multipart/form-data:

Content-Type: multipart/form-data; boundary="----MyGreatBoundary"
Content-Length: 7383

------MyGreatBoundary
Content-Type: text/plain; charset=utf-8
Content-Disposition: form-data; name=SaleId
5005558512577665890

------MyGreatBoundary
Content-Type: application/pdf
Content-Disposition: form-data; name=Attachments; filename="documentation.pdf"; filename*=utf-8''documentation.pdf
Array de bytes para documentation.pdf

------MyGreatBoundary
Content-Type: application/pdf
Content-Disposition: form-data; name=Attachments; filename="documentation2.pdf"; filename*=utf-8''documentation2.pdf
Array de bytes para documentation2.pdf

