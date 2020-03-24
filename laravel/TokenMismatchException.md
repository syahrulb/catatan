# Untuk menangani token mismatch ketika toke telah exp.
* buka file Handler.php -> lokasi file di app/Exceptions
* tambahkan kode berikut di fungsi (render) :

=======================================================================
if ($exception instanceof \Illuminate\Session\TokenMismatchException) {
    if ($request->expectsJson()) { #kondisi ketika pengguna ajax.
        return response()->json([
            'error' => 'Token mismatch'
        ], $exception->getStatusCode());
    }
    return redirect('/'); # kondisi ketika di local sistem
}#untuk token missmatch laravel.
======================================================================

* note : tambahan baris kode diatas sebelum baris kode :
==============================================
  return parent::render($request, $exception);
==============================================
