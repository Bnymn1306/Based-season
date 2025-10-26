{
  "@coinbase/x402": "latest",
  "x402-fetch": "latest",
  "x402-express": "latest"  // Express middleware
}
export const x402Payments = pgTable("x402_payments", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  userId: varchar("user_id").notNull().references(() => users.id),
  endpoint: text("endpoint").notNull(),  // "/api/tokens/premium"
  amount: text("amount").notNull(),      // "0.05" (USDC)
  txHash: text("tx_hash"),               // Blockchain tx hash
  status: text("status").notNull().default("pending"), // pending, verified, settled, failed
  metadata: jsonb("metadata"),           // Extra data (feature used, etc.)
  createdAt: timestamp("created_at").defaultNow().notNull(),
  settledAt: timestamp("settled_at"),
});
