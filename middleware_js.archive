export const config = {
  matcher: '/((?!_next|favicon.ico).*)',
};

export default function middleware(request) {
  const basicAuth = request.headers.get('authorization');

  if (basicAuth) {
    const authValue = basicAuth.split(' ')[1];
    const [user, pwd] = atob(authValue).split(':');
    if (user === process.env.AUTH_USER && pwd === process.env.AUTH_PASSWORD) {
      return;
    }
  }

  return new Response('Authentication required', {
    status: 401,
    headers: { 'WWW-Authenticate': 'Basic realm="Secure Area"' },
  });
}
