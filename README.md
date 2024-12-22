# Next.js 15 useRouter Hook SSR Issue

This repository demonstrates an uncommon bug in Next.js 15 related to the `useRouter` hook when used in components that aren't client-side rendered initially (Server-Side Rendering).

## Bug Description

The issue occurs when using `useRouter` within a component that's rendered on the server but then transitions to client-side rendering.  In certain scenarios, especially with fast navigation or dynamic routing, the `router` object might not be completely initialized, resulting in undefined behavior or navigation errors.

## Reproduction

1. Clone this repository.
2. Run `npm install`.
3. Run `npm run dev`.
4. Navigate to the `/about` page.
5. Click the 'Go back to Home' button.  Observe the behavior.  You might see errors or inconsistent behavior.

## Solution

The solution involves ensuring that the `useRouter` hook is used only after the component has fully mounted on the client.  This can be achieved using useEffect with dependency array set to empty to run it only after the initial render, and error handling to avoid runtime errors.   Alternatively, re-architecting the application to avoid server-side rendering the component where `useRouter` is used would prevent the issue.

## Additional Notes

This issue may not occur in all cases and might be dependent on specific routing configurations and application architecture. Proper error handling in your components is important.