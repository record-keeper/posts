# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-20T15:20:02.040566+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×55 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×16  [2026-05-20T15:04:29]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-05-20T15:04:29]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×16  [2026-05-20T15:04:29]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-20T15:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×61  [2026-05-20T14:19:55]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×17  [2026-05-20T11:33:46]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×45  [2026-05-20T10:00:24]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-20T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1907 actual=0.1429 gap=+0.0479`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-20T06:00:11]
- key: `DRIFT_BUCKET|drift ≤-30%: n=44 hit%=25.0% ROI=0.66 (コスト 13,000/回収 8,550)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-20T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=14 pred=0.0049 actual=0.0714 gap=-0.0665`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-20T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=11 pred=0.2239 actual=0.3636 gap=-0.1397`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-05-20T06:00:11]
- key: `ROI_STAT|S00: n=197 hit%=26.4% hit_CI[Bonf]=[18.4,36.3]% ROI=0.91 ROI_boot95=[0.65,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-20T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=197<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-20T06:00:11]
- key: `ROI_STAT|S01_NAKAANA1: n=51 hit%=31.4% hit_CI[Bonf]=[16.4,51.6]% ROI=0.85 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-20T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=51<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-05-20T06:00:11]
- key: `ROI_STAT|S02_TETSUBAN: n=33 hit%=48.5% hit_CI[Bonf]=[26.3,71.2]% ROI=0.91 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-20T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=33<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-20T06:00:11]
- key: `ORPHAN_SCAN|246 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-20T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=30.6% ROI=1.30 (コスト 8,700/回収 11,330)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-20T06:00:11]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=55 hit%=29.1% ROI=0.97 (コスト 13,600/回収 13,200)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.04MB / last modified 2026-05-20T15:19:07.082654+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
sed
2026-05-20 15:17:35,795 [INFO] scraper: odds2t: 28/30 parsed
2026-05-20 15:17:35,796 [INFO] scraper: odds2f: 15/15 parsed
2026-05-20 15:17:37,142 [INFO] scraper: odds_win: 6/6 parsed
2026-05-20 15:17:37,142 [INFO] scraper: fetch_race 17/10: boats=6 odds=189/191
2026-05-20 15:17:37,150 [INFO] predictor: CALIBRATION_MODE=on
2026-05-20 15:17:37,150 [INFO] predictor: combos: {'win': 6, '2t': 28, '3t': 120}
2026-05-20 15:17:37,159 [INFO] run_cycle: fetched 17/10 [scan]: 154 combos
2026-05-20 15:17:40,651 [INFO] scraper: odds3t: 120/120 parsed
2026-05-20 15:17:41,801 [INFO] scraper: odds3f: 20/20 parsed
2026-05-20 15:17:42,956 [INFO] scraper: odds2t: 30/30 parsed
2026-05-20 15:17:42,957 [INFO] scraper: odds2f: 15/15 parsed
2026-05-20 15:17:44,088 [INFO] scraper: odds_win: 6/6 parsed
2026-05-20 15:17:44,088 [INFO] scraper: fetch_race 21/10: boats=6 odds=191/191
2026-05-20 15:17:44,096 [INFO] predictor: CALIBRATION_MODE=on
2026-05-20 15:17:44,096 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-20 15:17:44,104 [INFO] run_cycle: fetched 21/10 [scan]: 156 combos
2026-05-20 15:17:44,227 [INFO] run_cycle: run_cycle done: 1 notifications
2026-05-20 15:18:05,676 [INFO] run_cycle: === run_cycle 15:18:05 ===
2026-05-20 15:18:05,676 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-20 15:18:05,676 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-20 15:18:05,767 [INFO] predictor: Models loaded OK
2026-05-20 15:18:06,147 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-20 15:19:06,572 [INFO] run_cycle: === run_cycle 15:19:06 ===
2026-05-20 15:19:06,572 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-20 15:19:06,572 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-20 15:19:06,619 [INFO] predictor: Models loaded OK
2026-05-20 15:19:07,051 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 58
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 58
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 11, 'scan': 24}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 87
  FINAL_MISSING: 55
  KS_ODDS_DRIFT: 43
  CIRCUIT_BREAKER_NO_ACTION: 17
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 2
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 31 | 11 | 9,300 | 12,180 | +2,880 | 1.31 |
| S01_NAKAANA1 | 27 | 6 | 5,400 | 5,380 | -20 | 0.996 |
| S02_TETSUBAN | 18 | 7 | 3,600 | 2,280 | -1,320 | 0.633 |

## 直近アラート (24h・新しい順)
```
[15:19:07] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 964}
[15:18:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 974}
[15:17:44] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 973}
[15:16:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 951}
[15:15:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 943}
[15:14:42] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 934}
[15:13:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 912}
[15:12:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 920}
[15:11:22] FINAL_MISSING: {"deadline": "2026-05-20T11:40:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052005011140", "sid": "S00"}
[15:11:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 5, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 919}
```

## 本日残レース: 54件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 90件 締切済
- 通知発射: scan=11 nid / final=10 nid / result=9 nid
- predictions: 9 / うち結果DB記録済: 9
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 088R | win | 1 | 0.5719 | 5.6 | 3.20 | 300 | scan=- drift=- | 13:40:23 |
| S01_NAKAANA1 | 087R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=- drift=- | 13:11:20 |
| S02_TETSUBAN | 165R | win | 1 | 0.5735 | 2.7 | 1.55 | 200 | scan=- drift=- | 13:01:21 |
| S01_NAKAANA1 | 175R | win | 1 | 0.5174 | 3.1 | 1.60 | 200 | scan=3.8 drift=-18.4% | 12:53:21 |
| S00 | 164R | win | 1 | 0.4111 | 7.9 | 3.25 | 300 | scan=6.0 drift=+31.7% | 12:31:20 |
| S00 | 149R | win | 1 | 0.5334 | 4.5 | 2.40 | 300 | scan=7.0 drift=-35.7% | 12:12:22 |
| S00 | 148R | win | 1 | 0.5123 | 4.0 | 2.05 | 300 | scan=6.0 drift=-33.3% | 11:40:35 |
| S00 | 162R | win | 1 | 0.4111 | 6.7 | 2.75 | 300 | scan=6.3 drift=+6.3% | 11:27:30 |
| S02_TETSUBAN | 211R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.3 drift=-4.3% | 10:45:32 |
| S02_TETSUBAN | 207R | win | 1 | 0.5174 | 2.5 | 1.29 | 200 | scan=2.2 drift=+13.6% | 20:22:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 44 | -2.8% | -76.3% | +148.9% | 18 | 9 | 31 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 457.3s |
| **Latency** (scan→final max) | 609.8s |
| **Traffic** (notifications 24h) | 58 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 287 | 0.4551 | 0.3066 | +0.1485 | 🟡+33% | 0.2313 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 199 | 0.4361 | 0.2714 | 0.2260 | 🔴-0.14 | 0.93 |
| S01_NAKAANA1 | win | 53 | 0.4894 | 0.3396 | 0.2367 | 🔴-0.06 | 0.934 |
| S02_TETSUBAN | win | 35 | 0.5113 | 0.4571 | 0.2530 | 🔴-0.02 | 0.854 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 14 | 0.0049 | 0.0714 | 🔴-0.0665 |
| 0.10-0.15 | 5 | 0.1288 | 0.2000 | 🔴-0.0712 |
| 0.15-0.20 | 6 | 0.1957 | 0.1667 | ✅+0.0291 |
| 0.20-0.30 | 11 | 0.2239 | 0.3636 | 🔴-0.1397 |
| 0.30-0.50 | 128 | 0.4243 | 0.2422 | 🔴+0.1821 |
| 0.50+ | 133 | 0.5399 | 0.3835 | 🔴+0.1565 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 16 | 0.775 |
| win | <5.0 | ✅learned | 34 | 0.832 |
| win | <10.0 | ✅learned | 27 | 0.548 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 0 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-05-20T15:20:02.040566+09:00_