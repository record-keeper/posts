# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-11-05T10:30:00.657256+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×28 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×85 (24h)
- 🔴 PSI_DRIFT_DETECTED×28 (24h)
- 🔴 CALIBRATION_DRIFT×20 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×1  [2026-11-05T10:29:59]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×9  [2026-11-05T10:05:27]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×9  [2026-11-05T10:05:27]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH  ×2  [2026-11-05T09:30:02]
- key: `CODE_AUDIT_SCRAPER_FAILURE_RATE_HIGH|直近 500 log行 で 3-retry 全敗 4 件 (閾値 3)`
- **FIX**: scraper 3-retry 全敗多発。boatrace.jp timeout or IP ban 疑い

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-05T06:00:45]
- key: `INSUFFICIENT_SAMPLE|S00: n=158<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-05T06:00:45]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-11-05T06:00:45]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=64<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-11-05T06:00:45]
- key: `ORPHAN_SCAN|178 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-05T06:00:45]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2290 actual=0.1111 gap=+0.1179`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-05T06:00:45]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=53 hit%=28.3% ROI=0.81 (コスト 12,800/回収 10,400)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-05T06:00:45]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=8 pred=0.1878 actual=0.0000 gap=+0.1878`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-05T06:00:45]
- key: `ROI_STAT|S00: n=158 hit%=29.1% hit_CI[Bonf]=[19.9,40.4]% ROI=0.78 ROI_boot95=[0.58,1.01]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-05T06:00:45]
- key: `ROI_STAT|S01_NAKAANA1: n=164 hit%=32.9% hit_CI[Bonf]=[23.4,44.1]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-11-05T06:00:45]
- key: `ROI_STAT|S02_TETSUBAN: n=64 hit%=45.3% hit_CI[Bonf]=[28.9,62.8]% ROI=1.05 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-05T06:00:45]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=38.2% ROI=1.02 (コスト 7,700/回収 7,860)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-05T06:00:45]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=75 hit%=42.7% ROI=1.13 (コスト 17,100/回収 19,260)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-11-05T06:00:45]
- key: `DRIFT_BUCKET|drift ≥+30%: n=37 hit%=16.2% ROI=0.48 (コスト 9,900/回収 4,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-05T06:00:45]
- key: `CALIBRATION_LIVE|bt=win: n=386 pred=0.4773 actual=0.3342 error=+0.1431 (+30%) brier=0.2350 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-05T06:00:45]
- key: `CALIBRATION_LIVE|S00(win): n=158 pred=0.4380 hit=0.2911 cal_err=+0.1468 brier=0.2214 BSS=-0.07 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-11-05T06:00:45]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=164 pred=0.4867 hit=0.3293 cal_err=+0.1574 brier=0.2373 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 17.57MB / last modified 2026-11-05T10:30:02.288630+09:00

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
/race/odds3t?rno=5&jcd=10&hd=20261105: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-05 10:28:42,351 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/odds3t?rno=5&jcd=10&hd=20261105: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-05 10:28:53,456 [INFO] scraper: odds3t: 120/120 parsed
2026-11-05 10:29:03,578 [INFO] scraper: odds3f: 20/20 parsed
2026-11-05 10:29:14,590 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=5&jcd=10&hd=20261105: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-05 10:29:25,621 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=5&jcd=10&hd=20261105: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-11-05 10:29:38,655 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=5&jcd=10&hd=20261105: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-11-05 10:29:38,655 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/odds2tf?rno=5&jcd=10&hd=20261105
2026-11-05 10:29:49,793 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/oddstf?rno=5&jcd=10&hd=20261105: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-11-05 10:29:58,916 [INFO] scraper: odds_win: 6/6 parsed
2026-11-05 10:29:58,916 [INFO] scraper: fetch_race 10/5: boats=6 odds=146/191
2026-11-05 10:29:58,919 [INFO] predictor: CALIBRATION_MODE=on
2026-11-05 10:29:58,919 [INFO] predictor: combos: {'win': 6, '3t': 120}
2026-11-05 10:29:58,922 [INFO] run_cycle: fetched 10/5 [scan]: 126 combos
2026-11-05 10:29:59,088 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 41
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 41
  }
]
```

## Phase別通知記録 (24h)
{'final': 15, 'result': 8, 'scan': 18}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 263
  FINAL_MISSING: 85
  PSI_DRIFT_DETECTED: 28
  CIRCUIT_BREAKER_NO_ACTION: 26
  CALIBRATION_DRIFT: 20
  STRATEGY_CI_FAIL: 17
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 15 | 2 | 4,500 | 2,130 | -2,370 | 0.473 |
| S01_NAKAANA1 | 19 | 8 | 3,800 | 3,960 | +160 | 1.042 |
| S02_TETSUBAN | 8 | 1 | 1,600 | 220 | -1,380 | 0.138 |

## 直近アラート (24h・新しい順)
```
[10:29:59] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 435}
[10:25:21] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 344, "n_recent": 42, "psi": 0.482}
[10:05:26] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[10:05:26] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 343, "n_recent": 43, "psi": 0.446}
[09:59:01] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 404}
[09:57:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 398}
[09:42:05] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 392}
[09:41:15] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 391}
[09:39:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 396}
[09:38:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 394}
```

## 本日残レース: 131件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 13件 締切済
- 通知発射: scan=1 nid / final=1 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 214R | win | 1 | 0.5476 | 2.3 | 1.26 | 200 | scan=- drift=- | 09:52:27 |
| S01_NAKAANA1 | 197R | win | 1 | 0.4994 | 3.4 | 1.70 | 200 | scan=3.5 drift=-2.9% | 20:23:15 |
| S01_NAKAANA1 | 194R | win | 1 | 0.4989 | 3.8 | 1.90 | 200 | scan=4.6 drift=-17.4% | 19:01:10 |
| S00 | 153R | win | 1 | 0.5334 | 5.1 | 2.72 | 300 | scan=- drift=- | 16:17:14 |
| S00 | 2210R | win | 1 | 0.0568 | 11.0 | 0.62 | 300 | scan=- drift=- | 15:11:42 |
| S01_NAKAANA1 | 097R | win | 1 | 0.4111 | 3.2 | 1.32 | 200 | scan=3.5 drift=-8.6% | 13:21:49 |
| S02_TETSUBAN | 2110R | win | 1 | 0.4111 | 2.7 | 1.11 | 200 | scan=- drift=- | 13:03:25 |
| S02_TETSUBAN | 092R | win | 1 | 0.5123 | 2.0 | 1.02 | 200 | scan=- drift=- | 10:55:26 |
| S02_TETSUBAN | 212R | win | 1 | 0.5735 | 2.4 | 1.38 | 200 | scan=- drift=- | 08:59:15 |
| S01_NAKAANA1 | 191R | win | 1 | 0.4989 | 3.1 | 1.55 | 200 | scan=3.5 drift=-11.4% | 17:40:03 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 18 | -6.4% | -54.4% | +54.8% | 6 | 3 | 10 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 479.8s |
| **Latency** (scan→final max) | 671.3s |
| **Traffic** (notifications 24h) | 41 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 386 | 0.4772 | 0.3342 | +0.1430 | 🟡+30% | 0.2351 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 157 | 0.4371 | 0.2866 | 0.2217 | 🔴-0.08 | 0.779 |
| S01_NAKAANA1 | win | 164 | 0.4867 | 0.3293 | 0.2373 | 🔴-0.07 | 0.766 |
| S02_TETSUBAN | win | 65 | 0.5502 | 0.4615 | 0.2619 | 🔴-0.05 | 1.049 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 8 | 0.1878 | 0.0000 | 🔴+0.1878 |
| 0.20-0.30 | 9 | 0.2290 | 0.1111 | 🔴+0.1179 |
| 0.30-0.50 | 139 | 0.4139 | 0.3022 | 🔴+0.1117 |
| 0.50+ | 225 | 0.5448 | 0.3778 | 🔴+0.1671 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 198 | 0.809 |
| win | <5.0 | ✅learned | 365 | 0.74 |
| win | <10.0 | ✅learned | 157 | 0.451 |
| win | <20.0 | ✅learned | 47 | 0.249 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-11-05T10:30:00.657256+09:00_